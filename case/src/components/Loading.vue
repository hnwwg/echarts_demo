<template>
  <div>
      <div class="loading" ref="loading"></div>
  </div>
</template>

<script>
import axios from "axios"
export default {
    data() {
        return {
            items:[],
            itemsNum:[],
        }
    },


    mounted(){

             axios.get("http://localhost:8080/data.json").then((res)=>{
                 this.items = res.data.items
                 this.itemsNum = res.data.itemsNum
    })




    window.setTimeout(()=>{
        
         let loadingCharts = this.$echarts.init(this.$refs.loading)

        let option = {
    title:{
        text: '异步请求+Loading+点击事件',
        left: 'center'
    },
    xAxis: {
        type: 'category',
        data: this.items
    },
    yAxis: {
        type: 'value'
    },
    series: [{
        data: this.itemsNum,
        type: 'bar',
        showBackground: true,
        backgroundStyle: {
            color: 'rgba(220, 220, 220, 0.8)'
        }
    }]
};
          loadingCharts.clear() //一般用于数据更新
           loadingCharts.hideLoading() //隐藏加载动画
         loadingCharts.setOption(option)
    },2000)



            let loadingCharts = this.$echarts.init(this.$refs.loading)

        let option = {
    title:{
        text: '异步请求+Loading',
        left: 'center'
    },
    xAxis: {
        type: 'category',
        data: []
    },
    yAxis: {
        type: 'value'
    },
    series: [{
        data: [],
        type: 'bar',
        showBackground: true,
        backgroundStyle: {
            color: 'rgba(220, 220, 220, 0.8)'
        }
    }]
};
       
        loadingCharts.showLoading() //显示加载动画
         loadingCharts.setOption(option)

    //   echartes的事件on（事件名，事件处理方法是一个函数）
      loadingCharts.on("click",(a)=>{
          window.alert(a.name)
      })

   
     
    }
}
</script>

<style>
.loading
{
    width: 500px;
    height: 500px;
}
</style>