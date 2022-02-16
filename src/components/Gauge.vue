<!--
 * @Date: 2022-02-12 12:51:08
 * @Author: 浩
 * @LastEditors: 浩
 * @FilePath: \highcharts\src\components\Gauge.vue
-->
<template>
  <div class="gauge chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title">安全等级</span>
      </div>
      <div id="highcharts-two" style="height: 275px"></div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "gauge",
  data() {
    return {
      // 仪表颜色
      optionColor: [
        // 0 ~ 1
        {
          linearGradient: {x1:1, x2:0, y1:1, y2:1},
          stops: [
            [0, "#ec9781"],
            [1, "#eed283"],
          ],
        },
        // 1 ~ 2
        {
          linearGradient: {x1:0, x2:1, y1:1, y2:1},
          stops: [
            [0, "#f5c684"],
            [1, "#f9de86"],
          ],
        },
        // 2 ~ 3
        {
          linearGradient: {x1:0, x2:1, y1:1, y2:1},
          stops: [
            [0, "#fadf86"],
            [1, "#e5e58b"],
          ],
        },
        // 3 ~ 4
        {
          linearGradient: {x1:0, x2:1, y1:1, y2:1},
          stops: [
            [0, "#ebe68a"],
            [1, "#b3dc96"],
          ],
        },
        // 4 ~ 5
        {
          linearGradient: {x1:1, x2:0, y1:1, y2:1},
          stops: [
            [0, "#cce191"],
            [1, "#78deac"],
          ],
        },
      ],
      // 数据颜色
      dataColor: ["#EC9481", "#F1C131", "#F1C131", "#6DB9D7", "#6ECFA6"],
      option: {
        chart: {
          type: "gauge",
          plotBackgroundColor: null,
          plotBackgroundImage: null,
          plotBorderWidth: 0,
          plotShadow: false,
        },
        title: {
          text: null,
        },
        credits: {
          enabled: false,
        },
        pane: {
          startAngle: -150,
          endAngle: 150,
          background: [],
        },
        plotOptions: {
          gauge: {
            dial: {
              backgroundColor: "#5c7faf",
              radius: "60%",
              baseLength: "20%",
              baseWidth: 10,
              rearLength: 0,
            },
            pivot: {
              backgroundColor: "#5c7faf",
            },
          },
        },
        yAxis: {
          min: 0,
          max: 5,
          title: {
            text: "安全等级",
            y: 180,
          },
          minorTickInterval: "auto",
          minorTickWidth: 1,
          minorTickLength: 6,
          minorTickPosition: "inside",
          minorTickColor: "#CCD6E3",
          tickPixelInterval: 60,
          tickWidth: 2,
          tickPosition: "inside",
          tickLength: 10,
          tickColor: "#CCD6E3",
          labels: {
            step: 1,
            rotation: "auto",
            distance: -35,
          },
          plotBands: [],
        },
        series: [
          {
            name: "安全等级",
            data: [],
            dataLabels: {
              useHTML: true,
              borderWidth: 0,
              y: 70,
              style: {},
            },
          },
        ],
      },
    };
  },
  mounted() {
    this.update();
  },
  methods: {
    update() {
      // 生成数据
      let num = 1 + Math.round(Math.random() * 4);
      // 添加数据
      this.option.series[0].data[0] = {
        name: "安全等级",
        y: num
      }
      // 添加样式
      this.option.series[0].dataLabels.style = {
        fontSize: "28px",
        color: this.dataColor[num - 1],
        fontWeight: "bold"
      }
      // 添加仪表盘样式
      for (let i = 0; i < num; i++) {
         this.option.yAxis.plotBands[i] = {
             from: i,
             to: i + 1,
             thickness: "20%",
             color: this.optionColor[i]
         }
      }
      // 补齐仪表盘样式
      for(let j = num; j < this.optionColor.length; j++) {
        this.option.yAxis.plotBands[j] = {
          from: j,
          to: j + 1,
          thickness: "20%",
          color: "#fff"
        }
      }
      // 生产图表
      HighCharts.chart("highcharts-two", this.option);
    },
  },
};
</script>

