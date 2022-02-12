<!--
 * @Date: 2022-02-12 12:38:23
 * @Author: 浩
 * @LastEditors: 浩
 * @FilePath: \highcharts\src\App.vue
-->
<template>
  <div id="app">
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
    scatter
  },
};
</script>

<style>
</style>
