<template>
  <div class="scatter chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title">运维数据概况</span>
      </div>
        <div
          id="highcharts-eight"
          style="min-width: 280px; height: 275px"
        ></div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "scatter",
  data() {
    return {
      option: {
        title: null,
        colors: ["rgba(167, 199, 242, .5)"],
        chart: {
          type: "scatter",
          zoomType: "xy",
          marginTop: 30,
          marginLeft: 33,
          marginRight: 30,
        },
        xAxis: {
          title: {
            text: "内存",
            align: 'high',
            offset: 0,
            x: 30,
            y: -14
          },
          startOnTick: true,
          endOnTick: true,
          showLastLabel: true,
          lineColor: "#000",
          lineWidth: 1,
          gridLineColor: "#e6e6e6",
          gridLineWidth: 1,
          tickPositioner: function() {
            return [0, 25, 50, 75, 100]
          }
        },
        yAxis: {      
          title: {
            enabled: true,
            align: "high",
            offset: 0,
            text: "CPU",
           rotation: 0,
            y: -12,
            x: 20
          },
          floor: 0,
          ceiling: 100,
          lineColor: "#000",
          lineWidth: 1,
          gridLineColor: "#e6e6e6",
          gridLineWidth: 1,
        },
        legend: {
          enabled: false,
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          pointFormat: "内存：{point.x}%<br/>CPU: {point.y}%<br/>",
        },
        series: [
          {
            name: "内存-CPU",
            data: [],
          },
        ],
        plotOptions: {
          scatter: {
            marker: {
              radius: 5
            }
          }
        }
      },
    };
  },
  mounted() {
    this.update();
  },
  methods: {
    update() {
      // 产生 100 ~ 300 个点
      let num = 100 + Math.round(Math.random() * 200);
      for (let i = 0; i < num; i++) {
        let newX = 1 + Math.round(Math.random() * 99);
        let newY = 1 + Math.round(Math.random() * 99);
        this.option.series[0].data[i] = { x: newX, y: newY};
      }
      HighCharts.chart("highcharts-eight", this.option);
    },
  },
};
</script>
