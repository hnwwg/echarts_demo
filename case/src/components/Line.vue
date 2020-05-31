<template>
  <div>
      <div class="line" ref="line"></div>
  </div>
</template>

<script>
export default {
    mounted(){
        let lineCharts = this.$echarts.init(this.$refs.line)

        let option = {
    title: {
        text: '未来一周气温变化+当点击最高温度变更数据',
        subtext: '纯属虚构'
    },
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data: ['最高气温', '最低气温']
    },
    toolbox: {
        show: true,
        feature: {
            dataZoom: {
                yAxisIndex: 'none'
            },
            dataView: {readOnly: false},
            magicType: {type: ['line', 'bar']},
            restore: {},
            saveAsImage: {}
        }
    },
    xAxis: {
        type: 'category',
        boundaryGap: false, //点线两边留不留白 false不留白  默认留白
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {
        type: 'value',
        axisLabel: {
            formatter: '{value} °C'
        }
    },
    series: [
        {
            name: '最高气温',
            type: 'line',
            data: [11, 11, 15, 13, 12, 13, 10],
            // 设置标记气泡
            markPoint: {
                data: [
                    {type: 'max', name: '最大值'}, //在最大值的地方显示气泡
                    {type: 'min', name: '最小值'}  //在最小值的地方显示气泡
                ]
            },
            // 设置标记线
            markLine: {
                data: [
                    {type: 'average', name: '平均值'} //所有值的平均值的地方显示一条虚线
                ]
            }
        },
        {
            name: '最低气温',
            type: 'line',
            data: [1, -2, 2, 5, 3, 2, 0],
            markPoint: {
                data: [
                    // 设置气泡显示的值，也可以设置气泡的位置 x轴位置，y轴位置
                    {name: '周最低', value: -2, xAxis: 1, yAxis: -1.5} 
                ]
            },
            markLine: {
                data: [
                    {type: 'average', name: '平均值'},
                    [{
                        symbol: 'none',
                        x: '90%',
                        yAxis: 'max'
                    }, {
                        symbol: 'circle',
                        label: {
                            position: 'start',
                            formatter: '最大值'
                        },
                        type: 'max',
                        name: '最高点'
                    }]
                ]
            }
        }
    ]
};
       lineCharts.setOption(option)
       lineCharts.on("click",(par)=>{
           if(par.value === 15){
                       let option = {
    title: {
        text: '未来一周气温变化+当点击最高温度变更数据',
        subtext: '纯属虚构'
    },
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data: ['最高气温', '最低气温']
    },
    toolbox: {
        show: true,
        feature: {
            dataZoom: {
                yAxisIndex: 'none'
            },
            dataView: {readOnly: false},
            magicType: {type: ['line', 'bar']},
            restore: {},
            saveAsImage: {}
        }
    },
    xAxis: {
        type: 'category',
        boundaryGap: false, //点线两边留不留白 false不留白  默认留白
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {
        type: 'value',
        axisLabel: {
            formatter: '{value} °C'
        }
    },
    series: [
        {
            name: '最高气温',
            type: 'line',
            data: [30, 28, 20, 16, 22, 25, 27],
            // 设置标记气泡
            markPoint: {
                data: [
                    {type: 'max', name: '最大值'}, //在最大值的地方显示气泡
                    {type: 'min', name: '最小值'}  //在最小值的地方显示气泡
                ]
            },
            // 设置标记线
            markLine: {
                data: [
                    {type: 'average', name: '平均值'} //所有值的平均值的地方显示一条虚线
                ]
            }
        },
        {
            name: '最低气温',
            type: 'line',
            data: [10, 8, 20, 11, 13, 22, 18],
            markPoint: {
                data: [
                    // 设置气泡显示的值，也可以设置气泡的位置 x轴位置，y轴位置
                    {name: '周最低', value: -2, xAxis: 1, yAxis: -1.5} 
                ]
            },
            markLine: {
                data: [
                    {type: 'average', name: '平均值'},
                    [{
                        symbol: 'none',
                        x: '90%',
                        yAxis: 'max'
                    }, {
                        symbol: 'circle',
                        label: {
                            position: 'start',
                            formatter: '最大值'
                        },
                        type: 'max',
                        name: '最高点'
                    }]
                ]
            }
        }
    ]
};
       lineCharts.setOption(option)
           }
       })
    }
}
</script>

<style>
.line
{
    width: 1000px;
    height: 500px
}
</style>