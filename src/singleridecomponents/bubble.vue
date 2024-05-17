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
      ['Sudden Braking', new Date('2022/02/14 1:22:10 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      ['Sudden Braking', new Date('2022/02/14 1:22:10:150 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      ['Sudden Braking', new Date('2022/02/14 1:22:51 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
      // ['Sudden Braking', new Date('2022/02/14 1:30:00 PM'), 94, "Anticipation", "Normal", "Sportive" ,72, 30],
      // ['Over Speed', new Date('2022/02/14 12:20 PM'),100, "Anticipation", "Normal", "Sportive" ,34, 62],
      // ['Over Speed', new Date('2022/02/14 1:27 PM'),97, "Anticipation", "Normal", "Sportive" ,20, 23],
      // ['Curve', new Date('2022/02/14 12:23 PM'), 93, "Anticipation", "Normal", "Sportive" ,50, 72],
      // ['Curve', new Date('2022/02/14 12:46 PM'), 100, "Anticipation", "Normal", "Sportive" ,22, 33],
      // ['Force Acceleration', new Date('2022/02/14 11:35 AM'),99, "Anticipation", "Normal", "Sportive" ,22, 66],
      // ['Sudden Braking', new Date('2022/02/14 11:24:00 AM'), 94, "Anticipation", "Normal", "Sportive" ,10, 20],
    ]
    const hexColors = {
    'Sudden Braking': '#f44336',
    'Over Speed': '#2196f3',
    'Curve': '#ffeb3b',
    'Force Acceleration': '#7bb57d',
    'Pedestrian Crossing': '#8b00ff',
    'School Zone': '#db67a6',
    'Stop Sign': '#f0b74f',
    'Priority': '#ffc0cb',
    'Animal Crossing': '#9bbdac',
    'Caution': '#807c7c',
    'Hill': '#ad8b7b',
    'Hill DownWards': '#8c488c',
    'Hill UpwnWards': '#91910d',
    'Icy Conditions': '#079494',
    'Intersection': '#993f3f',
    'Lane Merge': '#ffa07a',
    'Low Gear Area': '#5e5eb5',
    'Mobile use': '#c9c479',
    'Narrow Road': '#cd5c5c',
    'No OverTaking': '#b299c4',
    'Railway Crossing': '#808080',
    'Risk Of Grounding': '#a16ca1',
    'Slippery Roads': '#783434',
    'Traffic Light': '#e6853c',
    'Wind': '#008080',
    'Winding Road': '#714287',
    'Yield': '#adbd37',
    };
    const legendData = ["Over Speed","Curve","Force Acceleration","Pedestrian Crossing","School Zone","Stop Sign","Priority",
                        "Animal Crossing","Caution","Hill","Hill DownWards","Hill UpwnWards","Icy Conditions","Intersection", 
                        "Lane Merge","Low Gear Area","Mobile use","Narrow Road","No OverTaking","Railway Crossing",
                        "Risk Of Grounding","Slippery Roads","Traffic Light","Wind","Winding Road","Yield","Sudden Braking",].filter((cat) => data.some((item) => item[0] === cat));
    const chartOptions = ref ({
      tooltip: {
  height: 200, // set fixed height for tooltip
  show: true,
  formatter: function (params) {
    const date = params.value[1].toLocaleDateString();
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
      dataZoom: [{  type: 'slider',
                    showDataShadow: false,
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
                  },
                  { orient: 'vertical', 
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
          axisTick: {
            show: true,
            alignWithLabel: true,
            lineStyle: {color: '#6f7275', width: 1}
          },
          axisLine: {
            show:false,
            lineStyle: {color: '#bfbfbf',width: 1}
          },
          axisLabel: {show: true,
            rotate: 90,
            fontSize:13,
            align: 'right',
            color: '#6f7275',
          },
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
      title: {
              text: "COUNT",
              textStyle: {fontSize: 14,fontWeight: "bold",color: "#403e3a"},
              top: 55,
              right: 18,
             },
      legend: {
        show: data.length > 0,
        data: legendData,
      },
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
