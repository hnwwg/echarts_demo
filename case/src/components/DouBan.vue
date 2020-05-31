<template>
  <div>
    <div class="dou" ref="dou"></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
      let items = []
    axios.get("https://douban.uieee.com/v2/movie/top250").then((res) => {
        items = res.data.subjects;
        //  window.console.log(res.data)
         setData();
      })

    let douCharts = this.$echarts.init(this.$refs.dou);

    douCharts.showLoading();
    var setData = (function() {
      var option = {
        title: {
          text: "最近上映电影",
          left: "50%",
          textAlign: "center"
        },
        grid: {
          left: 0,
          right: 20,
          bottom: 100,
          top: 30
        },
        tooltip: {
          formatter: function(params) {
            if (params.componentSubType == "pictorialBar") {
              return (
                "电影：" +
                params.name +
                "</br> 豆瓣评分：" +
                (params.value * 1 + 10).toFixed(1)
              );
            }
          }
        },
        xAxis: {
          data: []
        },
        yAxis: {
          splitLine: {
            show: false
          },
          axisLine: {
            show: false
          }
        },
        series: [
          {
            type: "bar",
            barWidth: 1,
            data: [],
            animationDelay: function(idx) {
              return idx * 100;
            }
          },
          {
            type: "pictorialBar",
            symbolPosition: "end",
            symbolRotate: 165,
            symbolOffset: ["20%", "100%"],
            data: [],
            animationDelay: function(idx) {
              return idx * 100 + 500;
            }
          },
          {
            type: "graph",
            data: [
              {
                x: 0,
                y: 0,
                symbolSize: 0
              },
              {
                name: "btn",
                x: 0,
                y: 10,
                symbolSize: 30
              }
            ],
            itemStyle: {
              normal: {
                color: "transparent",
                borderWidth: 1,
                borderColor: "#555"
              }
            }
          }
        ]
      };
      var mark = 1;
      return function() {
        var pics = [];
        items.map((item)=>{
            // window.console.log(item)
            pics.push({
                value: ((item.rating.average || 0.1) - 10).toFixed(1),
                symbol:"image://https://images.weserv.nl/?url=" + item.images.small,
                symbolSize: ["48.75", "75"],
                name: item.title,
                id:item.id
            })
        })
        //  window.console.log(pics)
        if (mark % 2 == 0) {
          pics.sort(function(a, b) {
            return ((mark / 2) | 0) % 2 == 0
              ? b.value - a.value
              : a.value - b.value;
          });
        }
      
        option.series[0].data = pics;
        option.series[1].data = pics;
        douCharts.hideLoading();
        douCharts.setOption(option);
        mark++;
      };
    })();
    douCharts.on("click", function(params) {
        
      if (params.name === "btn") {
        setData();
      }else{
        // 点击跳转页面
        window.console.log(params)
        window.open("https://movie.douban.com/subject/"+params.data.id)
      }
    });
  }
};
</script>

<style>
.dou {
  width: 800px;
  height: 600px;
}
</style>