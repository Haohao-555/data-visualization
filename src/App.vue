<!--
 * @Date: 2022-02-12 12:38:23
 * @Author: 浩
 * @LastEditors: 浩
 * @FilePath: \highcharts\src\App.vue
-->
<template>
  <div id="app">
    <div class="main">
      <div class="h-conatiner">
        <!-- 环形图 -->
        <circular></circular>
        <!-- 仪表图 -->
        <gauge></gauge>
        <!-- 曲线图 -->
        <spline></spline>
        <!-- 柱状图 -->
        <column></column>
        <!-- 横向柱状图 -->
        <bar></bar>
        <!-- 散点图 -->
        <scatter></scatter>
      </div>
    </div>
  </div>
</template>
<script>
import circular from "./components/Circular.vue";
import gauge from "./components/Gauge.vue";
import spline from "./components/Spline.vue";
import column from "./components/Column.vue";
import bar from "./components/Bar.vue";
import scatter from "./components/Scatter.vue";
export default {
  name: "App",
  components: {
    circular,
    gauge,
    spline,
    column,
    bar,
    scatter,
  },
  data() {
    return {
      realNum: 0,
    };
  },
  mounted() {
    this.initLayout();
  },
  methods: {
    initLayout() {
      window.addEventListener("load", () => {
        this.realNum = document.querySelectorAll(".h-conatiner .chart").length;
        this.dealContainer();
      });
      window.addEventListener("resize", () => {
        this.dealContainer();
      });
    },
    dealContainer() {
      let cardList = document.querySelectorAll(".h-conatiner .chart");
      for (let i = this.realNum; i < cardList.length; i++) {
        cardList[i].remove();
      }
      let distance = cardList[0].offsetLeft;
      let w =
        window.innerWidth ||
        document.documentElement.clientWidth ||
        document.body.clientWidth;
      let cardWidth = cardList[0].clientWidth + 2 * distance;

      let num = (w / cardWidth).toFixed(1);

      let last = this.realNum % num;

      for (let j = last == 0 ? num : last; j < num; j++) {
        let card = document.createElement("div");
        card.className = "chart";
        document.querySelector(".h-conatiner").appendChild(card);
      }
    },
  },
};
</script>

<style>

.btn-active {
  border-color: #00428b !important;
  color: #00428b !important;
}
.el-button-group > .el-button:first-child {
  border-top-right-radius: 2px !important;
  border-bottom-right-radius: 2px !important;
}
.el-button-group > .el-button:last-child {
  border-top-left-radius: 2px !important;
  border-bottom-left-radius: 2px !important;
}
#app {
  color: #000;
  font-size: 12px;
  min-height: 100vh;
  min-width: 800px;
  background: #f3f3f3;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.main {
  display: block;
  flex: 1;
  flex-basis: auto;
  overflow: auto;
}
.h-conatiner {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  overflow-x: hidden;
}
.chart {
  width: 340px;
  height: 340px;
  margin-bottom: 10px;
  margin-right: 5px;
  margin-left: 5px;
}
.box-card {
  height: 100%;
  padding: 10px;
}
.el-card__body {
  padding: 6px 0px !important;
}
.el-card__header {
  padding: 10px 10px 10px 0px !important;
}
.chart {
  position: relative;
}
</style>
