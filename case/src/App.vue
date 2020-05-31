<template>
  <div id="app">

    <!-- 柱状图  多轴多图行混搭 -->
    <div> <BarChart /></div>

    <!-- 仪表盘 -->
    <div><Gauge /></div>

     <!-- 异步请求和loading -->
    <div><Loading /></div>

    <!-- 多图联动 -->
    <div><Ganged /></div>
   
    <!-- 线图 -->
    <div><LineChart /></div>
   
   <!-- 地图 -->
   <div><Map /></div>

   <!-- 豆瓣电影 -->
   <div><DouBan /></div>
  </div>
</template>

<script>
import BarChart from "./components/BarChart"
import Gauge from "./components/Gauge"
import Ganged from "./components/Ganged"
import Loading from "./components/Loading"
import LineChart from "./components/Line"
import Map from "./components/Map"
import DouBan from "./components/DouBan"
export default {
  name: 'App',
  components: {
    BarChart,
    Gauge,
    Ganged,
    Loading,
    LineChart,
    Map,
    DouBan
  },
}
</script>

<style>
#app
{
  width: 100%;
  display:inline-flex;
  flex-wrap: wrap;
}
</style>


