<template>
  <div id="container" style="width:300px; height: 180px;"></div>
  <div id="zzz" class="about"></div>
</template>

<script setup>
import * as echarts from 'echarts';
import { onMounted } from 'vue';

onMounted(() => {
  // 基于准备好的dom，初始化echarts实例
  var chartDom = document.getElementById('zzz');
  var myChart = echarts.init(chartDom);
  // 绘制图表
  var option;

  option = {
    title: {
      text: '未来一周气温变化'
    },
    tooltip: {
      trigger: 'axis'
    },
    legend: {},
    toolbox: {
      show: true,
      feature: {
        dataZoom: {
          yAxisIndex: 'none'
        },
        dataView: { readOnly: false },
        magicType: { type: ['line', 'bar'] },
        restore: {},
        saveAsImage: {}
      }
    },
    xAxis: {
      type: 'category',
      boundaryGap: false,
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    },
    yAxis: {
      type: 'value',
      axisLabel: {
        formatter: '{value} °C'
      }
    },
    series: [
      {
        name: 'Highest',
        type: 'line',
        data: [10, 11, 13, 11, 12, 12, 9],
        markPoint: {
          data: [
            { type: 'max', name: 'Max' },
            { type: 'min', name: 'Min' }
          ]
        },
        markLine: {
          data: [{ type: 'average', name: 'Avg' }]
        }
      },
      {
        name: 'Lowest',
        type: 'line',
        data: [1, -2, 2, 5, 3, 2, 0],
        markPoint: {
          data: [{ name: '周最低', value: -2, xAxis: 1, yAxis: -1.5 }]
        },
        markLine: {
          data: [
            { type: 'average', name: 'Avg' },
            [
              {
                symbol: 'none',
                x: '90%',
                yAxis: 'max'
              },
              {
                symbol: 'circle',
                label: {
                  position: 'start',
                  formatter: 'Max'
                },
                type: 'max',
                name: '最高点'
              }
            ]
          ]
        }
      }
    ]
  };

  option && myChart.setOption(option);
})

// 高德-天气API
window.onLoad = function () {
  var map = new AMap.Map('container');
}
var url = 'https://webapi.amap.com/maps?v=1.4.15&key=8c3dadb148bb72594ff3531e0194d49a&callback=onLoad';
var jsapi = document.createElement('script');
// jsapi.charset = 'utf-8';
jsapi.src = url;
document.head.appendChild(jsapi);
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 60vh;
    display: flex;
    align-items: center;
  }
}
</style>
