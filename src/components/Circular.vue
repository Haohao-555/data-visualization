<!--
 * @Date: 2022-02-12 12:45:00
 * @Author: 浩
 * @LastEditors: 浩
 * @FilePath: \highcharts\src\components\Circular.vue
-->
<template>
  <div class="circular chart">
    <el-card class="box-card" shadow="always">
      <div slot="header">
        <span class="title">终端概况</span>
      </div>
      <div class="container">
        <el-button-group>
          <el-button
             size="mini"
            style="margin-right: 10px"
            :class="[btn == 0 ? 'btn-active' : '']"
            @click="btn = 0"
            >终端统计</el-button
          >
          <el-button
            size="mini"
            :class="[btn == 1 ? 'btn-active' : '']"
            @click="btn = 1"
            >终端合理统计</el-button
          >
        </el-button-group>
        <div id="highcharts-one" style="min-width: 318px; height: 270px"></div>
      </div>
    </el-card>
  </div>
</template>
<script>
import HighCharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
highchartsMore(HighCharts);
export default {
  name: "chartone",
  data() {
    return {
      // 设置数据的阈值
      min: 300,
      max: 1000,

      btn: 0,
      command: 0,
      // chart 实例
      chart: null,
      // 配置选项
      option: {
        legend: {
          symbolRadius: 0,
          itemMarginBottom: 12
        },
        title: {
          floating: true,
          useHTML: true,
          style: {
            fontSize: "11px",
            color: "#809CC1",
            textAlign: "center",
          },
        },
        credits: {
          enabled: false,
        },
        plotOptions: {
          pie: {
            allowPointSelect: false,
            cursor: "pointer",
            size: 150,
            dataLabels: {
              enabled: true,
              format: "<b style='font-weight: normal;'>{point.name}:</b><br/>{point.y}",
              connectorWidth: 1,
              connectorPadding: 0,
              crookDistance: "10%",
              distance: 10,
            },
            showInLegend: true,
          },
        },
        series: [
          {
            type: "pie",
            innerSize: "70%",
            name: "终端数",
          },
        ],
      },
      // 数据
      dataList: [],
      // 终端统计（格式）
      statistFormat: [
        { name: "在线终端", y: 0, color: "#63adff" },
        { name: "离线终端", y: 0, color: "#ccd6e3" },
        { name: "异常终端", y: 0, color: "#ff5d6a" },
      ],
      // 合理终端显示（格式）
      reasonFormat: [
        { name: "在线终端", y: 0, color: "#63adff" },
        { name: "离线终端", y: 0, color: "#ccd6e3" },
      ],
    };
  },
  watch: {
    btn() {
      this.update();
    },
  },
  mounted() {
    this.update();
  },
  methods: {
    update() {
      // 判断
      let num = this.btn == 0 ? 3 : 2;
      let format = this.btn == 0 ? this.statistFormat : this.reasonFormat;
      let sum = 0;
      // 随机生成数据
      for (let i = 0; i < num; i++) {
        let newY = this.min + Math.round(Math.random() * (this.max - this.min));
        format[i].y = newY;
        sum += newY;
      }
      // 设置标题
      this.option.title.text = `<i class='el-icon-monitor icon'></i></br><b>终端总数：${sum}</b>`;

      this.dataList = format;
      
      // 初始化
      let chart = HighCharts.chart("highcharts-one", this.option, function (c) {
        c.setTitle({
          y: c.series[0].center[1] + parseInt(c.title.styles.fontSize) / 2 - 35,
        });
      });
      chart.series[0].setData(this.dataList);
    },
    handleCommand(command) {
      if (command != "end-cmd-2") {
        this.btn = command;
      } else {
        this.$message("菜单项command：" + command);
      }
    },
  },
};
</script>
<style>
.icon {
  color: "#809CC1";
  font-size: 25px;
}
</style>
