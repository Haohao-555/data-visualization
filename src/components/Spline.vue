<template>
  <div class="spline chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title">数据资产概况</span>
      </div>
      <div class="container">
        <el-button-group>
          <el-button
            size="mini"
            style="margin-right: 8px"
            :class="[btn == 0 ? 'btn-active' : '']"
            @click="btn = 0"
          >
            加解密操作次数统计
          </el-button>
          <el-button
            size="mini"
            :class="[btn == 1 ? 'btn-active' : '']"
            @click="btn = 1"
          >
            解密个人排行榜Top10
          </el-button>
        </el-button-group>
        <div id="highcharts-five" style="height: 275px; min-width: 318px"></div>
      </div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "spline",
  data() {
    return {
      btn: 0,

      // 数据范围
      max: 3000,
      min: 500,

      // 配置选项
      option: {
        title: {
          text: null,
        },
        legend: {
          itemMarginBottom: 12,
          align: "left",
        },
        chart: {
          type: "spline",
        },
        xAxis: {
          type: "datetime",
          dateTimeLabelFormats: {
            day: "%m/%d",
          },
          tickInterval:  24 * 3600 * 1000,
          // minTickInterval: 24 * 3600 * 1000
          labels: {
            align: "center",
            style: {
               fontSize: "8px",
            },
          },
        },
        yAxis: {
          title: {
            text: null,
          },
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          shared: true,
          crosshairs: [
            {
              width: 1,
              color: "#cccccc",
            },
          ],
          dateTimeLabelFormats: {
            day: "%m/%d",
          },
        },
        plotOptions: {
          series: {
            pointStart: Date.UTC(2010, 1, 11), // 开始值
            pointInterval: 24 * 3600 * 1000, // 间隔一天
          },
          spline: {
            marker: {
              enabled: false,
            },
          },
        },
      },

      // 数据
      dataList: [],

      // 加密操作数据
      operaFormat: [
        {
          name: "加密文件",
          data: [],
          color: "#7cb5ec",
        },
        {
          name: "解密文件",
          data: [],
          color: "#f08626",
        },
      ],
      // Top 10
      topFormat: [
        {
          name: "排行一",
          data: [],
          color: "#7cb5ec",
        },
        {
          name: "排行二",
          data: [],
          color: "#f08626",
        },
        {
          name: "排行三",
          data: [],
          color: "#90ed7d",
        },
        {
          name: "排行四",
          data: [],
          color: "#f7a35c",
        },
        {
          name: "排行五",
          data: [],
          color: "#8085e9",
        },
        {
          name: "排行六",
          data: [],
          color: "#f15c80",
        },
        {
          name: "排行七",
          data: [],
          color: "#e4d354",
        },
        {
          name: "排行八",
          data: [],
          color: "#2b908f",
        },
        {
          name: "排行九",
          data: [],
          color: "#f45b5b",
        },
        {
          name: "排行十",
          data: [],
          color: "#8edfd8",
        },
      ],
    };
  },
  mounted() {
    this.updata();
  },
  watch: {
    btn() {
      this.updata();
    },
  },
  methods: {
    updata() {
      // 判断
      let num = this.btn == 0 ? 2 : 10;
      let format = this.btn == 0 ? this.operaFormat : this.topFormat;
      // 生成数据
      for (let i = 0; i < num; i++) {
        // 产生 7个随机数
        for (let j = 0; j < 7; j++) {
          let newY =
            this.min + Math.round(Math.random() * (this.max - this.min));
          format[i].data[j] = { y: newY };
        }
      }
      this.dataList = format;
      this.option.series = this.dataList;
      HighCharts.chart("highcharts-five", this.option);
    },
  },
};
</script>

