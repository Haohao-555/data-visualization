<template>
  <div class="column chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title"> 文档流转概况 </span>
      </div>
      <div class="container">
        <el-button-group>
          <el-button
            size="mini"
            style="margin-right: 8px"
            :class="[btn == 0 ? 'btn-active' : '']"
            @click="btn = 0"
          >
            文档流转统计
          </el-button>
          <el-button size="mini"  :class="[btn == 1 ? 'btn-active' : '']" @click="btn = 1">
            文档流转个人排行榜Top10
          </el-button>
        </el-button-group>
        <div id="highcharts-six" style="min-width: 318px; height: 260px"></div>
      </div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "column",
  data() {
    return {
      btn: 0,
      // 随机数范围
      max: 2000,
      min: 500,
      option: {
        // 标题
        title: null,
        colors: ["#a7c7f2"],
        // 图表类型
        chart: {
          type: "column",
        },
        // x轴
        xAxis: {
          title: null,
          categories: [],
          labels: {
            // 步长
            step: 1,
          },
        },
        // y轴
        yAxis: {
          title: null,
          ceiling: 2000,
        },
        // 数据
        series: [
          {
            data: [],
          },
        ],
        // 底部样式
        legend: {
          enabled: false,
        },
        credits: {
          enabled: false,
        },
        // 提示
        tooltip: {
          headerFormat: null,
          pointFormat: "{point.y}",
        },
      },
    };
  },
  mounted() {
    this.update();
  },
  watch: {
     btn() {
       this.update();
     }
  },
  methods: {
    update() {
      // 判断
      let num = this.btn == 0 ? 5 : 10;
      
      // 数据清空
      this.option.series[0].data = [];
      this.option.xAxis.categories = [];
      // 生成数据
      for (let i = 0; i < num; i++) {
        let newY = this.min + Math.round(Math.random() * (this.max - this.min));
        let newX = 1 + Math.round(Math.random() * (num - 1));
        this.option.series[0].data[i] = newY;
        this.option.xAxis.categories[i] = newX;
      }
      HighCharts.chart("highcharts-six", this.option);
    },
  },
};
</script>

