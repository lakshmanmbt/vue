<template>
  <v-chart class="chart" :option="chartOptions" autoresize />
</template>

<script>

import VChart, { THEME_KEY } from 'vue-echarts';
import { ref, defineComponent } from 'vue';
import  'echarts'

export default defineComponent({
  name: 'HelloWorld',    
  components: {VChart},
  provide: {[THEME_KEY]: 'light'},
  setup() {
    const data = [ 
      ['Sudden Braking', new Date('2022/02/14 1:22:9:750 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      ['Sudden Braking', new Date('2022/02/14 1:22:10:150 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      ['Sudden Braking', new Date('2022/02/14 12:22:10:150 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      ['Sudden Braking', new Date('2022/02/14 12:22:10:150 PM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
    ]
    const hexColors = {
    'Sudden Braking': '#f44336',
    };
    const legendData = ["Sudden Braking",].filter((cat) => data.some((item) => item[0] === cat));
    const chartOptions = ref ({
      tooltip: {
  height: 200, // set fixed height for tooltip
  show: true,
  formatter: function (params) {
    const date = params.value[1].toLocaleDateString();
    // const time = params.value[1].toLocaleTimeString('en-US', {hour: 'numeric', minute: 'numeric', second: 'numeric', hour12: true});
    // const time = params.value[1].toISOString().substr(11, 12).replace(/\./, ':');
    // const time = params.value[1].toISOString().substr(11, 12);
    const time = params.value[1].toLocaleTimeString();
    const size = params.value[2];
// Generate tooltip content
const tooltipContent =
  '<div style="text-align: left;">' +
  '<span style="display: inline-block; width: 120px;">Date: </span>' + date + '<br>' +
  '<span style="display: inline-block; width: 120px;">Time: </span>' + time + '<br>' +
  '<span style="display: inline-block; width: 120px;">Risk Value: </span>' + size + '<br>' +
  '</div>';

return tooltipContent;
}
},
      dataZoom: [{ orient: 'vertical', 
                    type: 'slider',
                    showDataShadow: false,
                    left: '10%',
                    top: '8%',
                    bottom: 180,
                    height: 500,
                    width: 12,
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
                  }
                ],
      xAxis: {
          type: 'category',
          boundaryGap: true,
          splitLine: { 
            alignWithLabel: true,
            show: true,
            lineStyle: {type: 'line',color: '#bfbfbf',offset: 0},
          },
          axisPointer: {
                  type: 'line',
                  lineStyle: {color: '#6f7275',width: 1}
          }
            },
      yAxis: {
          type: 'time',
          lineStyle: {color: '#bfbfbf',width: 1},
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
      grid: {bottom: '20%',
            left : '20%',
            right : '10%'},
      visualMap: {
        show: data.length > 0,
        top: 85,
        right: 25,
        seriesIndex: 0,
        dimension: 0,
        pieces: legendData.map((cat) => {
          return {
            value: cat,
            color: hexColors[cat],
            label: "" + data.filter(item => item[0] === cat).length
          };
        }),
        outOfRange: {
          color: "#999",
        },
      },
      series: [
        {
          label: { show: true },
          type: 'scatter',
          data: data.map((item) => ({
            name: item[0],
            value: [item[0], item[1], item[2], item[3], item[4], item[5], item[6], item[7]],
            itemStyle: {color: hexColors[item[0]],borderColor: '#6e706f',borderWidth: 1},
          })),
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
      showSymbol: data.length > 0,
        },
      ],
    });

    return { chartOptions };
  },
}); 
</script>

<style scoped>
  .chart {height: 100vh;}
</style>
