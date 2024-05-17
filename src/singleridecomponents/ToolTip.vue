<template>
  <v-chart class="chart" :option="chartOptions" autoresize />
  
</template>
<script>

import VChart, { THEME_KEY } from 'vue-echarts';
import { ref, defineComponent } from 'vue';
import * as echarts from 'echarts';

export default defineComponent({
  name: 'HelloWorld',    
  components: {VChart},
  provide: {[THEME_KEY]: 'light'},
  setup() {
    const data = [
  ['', new Date(''), 0],
  ['Sudden Braking', new Date('2022/02/14 11:22:00 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
  ['Sudden Braking', new Date('2022/02/14 11:24:00 AM'), 94, "Anticipation", "Normal", "Sportive" ,10, 20],
  ['Sudden Braking', new Date('2022/02/14 1:30:00 PM'), 94, "Anticipation", "Normal", "Sportive" ,72, 30],
  ['Over Speed', new Date('2022/02/14 12:20 PM'),100, "Anticipation", "Normal", "Sportive" ,34, 62],
  ['Over Speed', new Date('2022/02/14 1:27 PM'),97, "Anticipation", "Normal", "Sportive" ,20, 23],
  ['Curve', new Date('2022/02/14 12:23 PM'), 93, "Anticipation", "Normal", "Sportive" ,50, 72],
  ['Curve', new Date('2022/02/14 12:46 PM'), 100, "Anticipation", "Normal", "Sportive" ,22, 33],
  ['Force Acceleration', new Date('2022/02/14 11:35 AM'),99, "Anticipation", "Normal", "Sportive" ,22, 66],
]
       
    const  chartOptions = ref ({
      tooltip: {
  height: 200,
  show: true,
  formatter: function(params) {
    const date = params.value[1].toLocaleDateString();
    const time = params.value[1].toLocaleTimeString();
    const size = params.value[2];
    const rstyle = params.value[3];
    const dstate = params.value[4];
    const dstyle = params.value[5];
    const speedLimit = params.value[6];
    const speed = params.value[7];

    // Create ECharts chart instance
    const chart = echarts.init(document.createElement('div'));

    // Set chart options
    const options = {
      xAxis: {
        type: 'category',
        data: ['Speed Limit', 'Speed'],
      },
      yAxis: {
        type: 'value',
      },
      series: [
        {
          type: 'bar',
          barWidth: '30%',
          data: [speedLimit, speed],
          itemStyle: {
            color: function(params) {
              const colorList = ['#DC143C', '#3CB371'];
              return colorList[params.dataIndex];
            },
          },
          label: {
            show: true,
            position: 'top',
            formatter: '{c}',
          },
        },
      ],
    };

    // Set chart options
    chart.setOption(options);

    // Get chart image data URL
    const dataURL = chart.getDataURL({ pixelRatio: 2 });

    // Generate tooltip content
    const tooltipContent =
      '<div style="text-align: left;">' +
      '<span style="display: inline-block; width: 120px;">Date: </span>' +
      date +
      '<br>' +
      '<span style="display: inline-block; width: 120px;">Time: </span>' +
      time +
      '<br>' +
      '<span style="display: inline-block; width: 120px;">Risk Value: </span>' +
      size +
      '<br>' +
      '<span style="display: inline-block; width: 120px;">Risk Style: </span>' +
      rstyle +
      '<br>' +
      '<span style="display: inline-block; width: 120px;">Driver State: </span>' +
      dstate +
      '<br>' +
      '<span style="display: inline-block; width: 120px;">Driving Style: </span>' +
      dstyle +
      '<br>' +
      '<img src="' +
      dataURL +
      '" />' +
      '</div>';

    return tooltipContent;
  },
},
      dataZoom: 
    [
    {
      orient: 'vertical',
      startValue: '0',
      left: '10%',
      top: '8%',
      height: '70%',
    },
    {
      type: 'inside'
    },
    {
      orient: 'horizontal',
      startValue: '0'
    },
    {
      type: 'inside'
    }
    ],
    xAxis: {
          type: 'category',
          boundaryGap: false,

          axisTick: {
            alignWithLabel: false,
            lineStyle: {
              color: '#6f7275',
              width: 1
            }
          },
          axisLine: {
            show:false,
            lineStyle: {
              color: '#6f7275',
              width: 1
            }
          },
          axisLabel: {show: true,
            rotate: 90,
            fontSize:10,
            align: 'right'
          },
          splitLine: { 
            show: true,
            lineStyle: {
              type: 'line',
              color: '#bfbfbf',
              offset: 0

            },
          },
          axisPointer: {
                  type: 'line',
                  lineStyle: {
                  color: '#6f7275',
                  width: 1
                  }
  }
                  },
      grid: {bottom: '20%',
            left : '20%',
            right : '10%'},


      yAxis: {
       type: 'time',
       lineStyle: {
              color: '#bfbfbf',
              width: 1
            },
       
        axisLabel: {
            formatter: function(value) {
              const date = new Date(value)
              let hours = date.getHours()
              let minutes = date.getMinutes()
              const ampm = hours >= 12 ? 'PM' : 'AM'
              hours = hours % 12
              hours = hours ? hours : 12
              minutes = minutes < 10 ? '0' + minutes : minutes
              const time = hours + ':' + minutes + ' ' + ampm
              return time
            }
          }
      },
      series: [
    {
      label: { show: true },
      type: "scatter",
      data: data,
      symbolSize: function (data) {

        let symbol = 0;

        if(data[2] == 91){
          symbol = 1*10
        } else if(data[2] == 92){
          symbol = 2*10
        }else if(data[2] == 93){
          symbol = 3*10
        }else if(data[2] == 94){
          symbol = 4*10
        }else if(data[2] == 95){
          symbol = 5*10
        }else if(data[2] == 96){
          symbol = 6*10
        }else if(data[2] == 97){
          symbol = 7*10
        }else if(data[2] == 98){
          symbol = 8*10
        }else if(data[2] == 99){
          symbol = 9*10
        }else if(data[2] == 100){
          symbol = 10*10
        }else{
          symbol = 0
        }
        return symbol;
      },
      itemStyle: {
        color: function (params) {
          const categories = [
            "",
            "Sudden Braking",
            "Over Speed",
            "Curve",
            "Force Acceleration",
            
          ];
          const colors = ["#5c5c5c", "#f44336", "#2196f3", "#ffeb3b", "#4caf50"];
          const categoryIndex = categories.indexOf(params.data[0]);
          return colors[categoryIndex];
        },
        borderColor: "black",
        borderWidth: 1,
      },
    },
  ]
    })
  
      return {chartOptions };
    },
  }); 
  </script>
  
  <style scoped>
  .chart {height: 100vh;}
  </style>
  