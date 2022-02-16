<template>
  <div class="bar chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title">行为管理概况</span>
      </div>
      <div class="container">
        <el-button-group>
          <el-button
            size="mini"
            style="margin-right: 8px"
            :class="[btn == 0 ? 'btn-active' : '']"
            @click="btn = 0"
            >应用程序活跃度统计</el-button
          >
          <el-button
            size="mini"
            :class="[btn == 1 ? 'btn-active' : '']"
            @click="btn = 1"
            >上网浏览统计</el-button
          >
        </el-button-group>
        <div
          id="highcharts-seven"
          style="min-width: 318px; height: 260px"
        ></div>
      </div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "bar",
  data() {
    return {
      btn: 0,
      min: 3600,
      max: 21600,
      appxa: [
        "有道云笔记",
        "QQ音乐",
        "企业微信",
        "Outlook邮箱",
        "腾讯微信",
        "Office",
        "钉钉",
        "谷歌浏览器",
        "新浪微博",
      ],
      webxa: [
        "360浏览器",
        "谷歌浏览器",
        "edge",
        "QQ浏览器",
        "火狐浏览器",
        "IE浏览器",
      ],
      option: {
        chart: {
          type: "bar",
        },
        colors: ["#70aeea"],
        title: {
          text: null,
        },
        legend: {
          enabled: false,
        },
        credits: {
          enabled: false,
        },
        xAxis: {
          lineWidth: 0,
          gridLineWidth: 0,
        },
        yAxis: {
          min: 0,
          title: {
            text: null,
          },
          labels: {
            enabled: false,
          },
          lineWidth: 0,
          gridLineWidth: 0,
        },
        tooltip: {
          pointFormat:
            '<span style="color:#A7C7F2">\u25CF</span>{series.name} : {point.time}<br/>',
        },
        plotOptions: {
          series: {
            borderRadius: 6,
          },
          bar: {
            dataLabels: {
              enabled: true,
              align: "left",
              style: {
                fontWeight: "normal",
                textOutline:"none"
              },
              formatter: function () {
                return this.point.time;
              },
            },
          },
        },
        series: [
          {
            name: "使用时间",
            data: [],
          },
        ],
      },
    };
  },
  mounted() {
    this.update();
  },
  watch: {
    btn() {
      this.update();
    },
  },
  methods: {
    update() {
      let num = this.btn == 0 ? 9 : 6;
      let nameList = this.btn == 0 ? this.appxa : this.webxa;
      // 清空数据
      this.option.series[0].data = [];
      for (let i = 0; i < num; i++) {
        let time = this.min + Math.round(Math.random() * (this.max - this.min));
        this.option.series[0].data[i] = {
          name: nameList[i],
          y: time,
          time: this.fomatDate(time),
          dataLabels: {
            inside: time > 7200 ? true: false,
            style: {
              color: time > 7200 ? "#fff" : "#000"
            }
          },
        };
      }
      // 设置 x轴
      this.option.xAxis.categories = nameList;
      HighCharts.chart("highcharts-seven", this.option);
    },
    // 时间换算
    fomatDate(sec) {
      // 小时
      let h = Math.floor(sec / 3600);
      let m = Math.floor((sec % 3600) / 60);
      return `${h}小时${m}分钟`;
    },
  },
};
</script>


