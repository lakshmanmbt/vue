<template>
    <div>
      <div ref="chart" style="height: 400px;"></div>
    </div>
  </template>
  
  <script>
  import * as echarts from 'echarts';
  
  export default {
    mounted() {
      this.initChart();
    },
    methods: {
      initChart() {
        const inputData = [
          ['00:00:00', 3],
  ['00:00:01', 8],
  ['00:00:02', 5],
  ['00:00:03', 12],
  ['00:00:04', 9],
  ['00:00:05', 4],
  ['00:00:06', 7],
  ['00:00:07', 6],
  ['00:00:08', 2],
  ['00:00:09', 11],
  ['00:00:10', 13],
  ['00:00:11', 7],
  ['00:00:12', 9],
  ['00:00:13', 6],
  ['00:00:14', 8],
  ['00:00:15', 3],
  ['00:00:16', 4],
  ['00:00:17', 10],
  ['00:00:18', 6],
  ['00:00:19', 5],
  ['00:00:20', 8],
  ['00:00:21', 2],
  ['00:00:22', 7],
  ['00:00:23', 5],
  ['00:00:24', 9],
  ['00:00:25', 1],
  ['00:00:26', 3],
  ['00:00:27', 6],
  ['00:00:28', 10],
  ['00:00:29', 12],
  ['00:00:30', 7],
  ['00:00:31', 2],
  ['00:00:32', 5],
  ['00:00:33', 9],
  ['00:00:34', 4],
  ['00:00:35', 8],
  ['00:00:36', 6],
  ['00:00:37', 3],
  ['00:00:38', 7],
  ['00:00:39', 1],
  ['00:00:40', 11],
  ['00:00:41', 9],
  ['00:00:42', 4],
  ['00:00:43', 6],
  ['00:00:44', 10],
  ['00:00:45', 5],
  ['00:00:46', 8],
  ['00:00:47', 2],
  ['00:00:48', 7],
  ['00:00:49', 3],
  ['00:00:50', 4],
  ['00:00:51', 6],
  ['00:00:52', 5],
  ['00:00:53', 1],
  ['00:00:54', 12],
  ['00:00:55', 9],
  ['00:00:56', 7],
  ['00:00:57', 3],
  ['00:00:58', 8],
  ['00:00:59', 6],
  ['00:01:00', 5],
  ['00:01:01', 2],
  ['00:01:02', 7],
  ['00:01:03', 4],
  ['00:01:04', 10],
  ['00:01:05', 9],
  ['00:01:06', 8],
  ['00:01:07', 5],
  ['00:01:08', 6],
  ['00:01:09', 3],
  ['00:01:10', 11],
  ['00:01:11', 1],
  ['00:01:12', 4],
  ['00:01:13', 9],
  ['00:01:14', 7],
  ['00:01:15', 6],
  ['00:01:16', 5],
  ['00:01:17', 2],
  ['00:01:18', 8],
  ['00:01:19', 3],
  ['00:01:20', 6],
  ['00:01:21', 10],
  ['00:01:22', 9],
  ['00:01:23', 7],
  ['00:01:24', 3],
  ['00:01:25', 5],
  ['00:01:26', 8],
  ['00:01:27', 4],
  ['00:01:28', 1],
  ['00:01:29', 7]
        ];
  
        // Extract time and g-force data from the input array
        const timeData = inputData.map(item => item[0]);
        const gForceData = inputData.map(item => item[1]);
  
        const chartDom = this.$refs.chart;
        const myChart = echarts.init(chartDom);
        
        const option = {
        tooltip: {
          trigger: 'axis',
          formatter: '{b}<br>{c} g-force', // Display tooltip with time and g-force value
        },
          xAxis: {
            type: 'category',
            data: timeData,
            axisLabel: {
            interval: 'auto', // Automatically adjust interval to fit all labels
          },
          },
          yAxis: {
            type: 'value',
            axisLabel: {
              formatter: '{value}g', // Show percentage symbol on y-axis
            },
          },
          dataZoom: [{  type: 'slider',
                    showDataShadow: false,
                    startValue: 20,
                    endValue: 65,
                    bottom: 10,
                    height: 12,
                    borderColor: 'transparent',
                    backgroundColor: 'transparent',
                    fillerColor: '#9fa7e3',
                    handleStyle: {
                      color: '#9fa7e3',
                      borderColor: 'transparent',
                      borderWidth: 0
                    },
                    dataBackground: {
                      areaStyle: {
                        color: '#e2e2e2'
                      },
                      lineStyle: {
                        opacity: 0
                      }
                    }
                  },],
          series: [{
            data: gForceData,
            type: 'line',
            lineStyle: { // Customize line thickness
              width: 1, // Set line thickness (default: 2)
            },
          }],
        };
  
        myChart.setOption(option);
      },
    },
  };
  </script>
  
  <style>
  </style>
  