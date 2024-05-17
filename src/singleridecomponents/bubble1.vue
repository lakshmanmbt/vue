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
  ['', new Date(''), 0],
  ['Sudden Braking', new Date('2022/02/14 11:22:00 AM'), 91, "Anticipation", "Normal", "Sportive" ,50, 60],
  ['Sudden Braking', new Date('2022/02/14 11:24:00 AM'), 94, "Anticipation", "Normal", "Sportive" ,10, 20],
  ['Sudden Braking', new Date('2022/02/14 1:30:00 PM'), 94, "Anticipation", "Normal", "Sportive" ,72, 30],
  ['Over Speed', new Date('2022/02/14 12:20 PM'),100, "Anticipation", "Normal", "Sportive" ,34, 62],
  ['Over Speed', new Date('2022/02/14 1:27 PM'),97, "Anticipation", "Normal", "Sportive" ,20, 23],
  ['Curve', new Date('2022/02/14 12:23 PM'), 93, "Anticipation", "Normal", "Sportive" ,50, 72],
  ['Curve', new Date('2022/02/14 12:46 PM'), 100, "Anticipation", "Normal", "Sportive" ,22, 33],
  ['Force Acceleration', new Date('2022/02/14 11:35 AM'),99, "Anticipation", "Normal", "Sportive" ,22, 66],
  [' ', new Date(''), 0],
]
       
    const  chartOptions = ref ({
      tooltip: {
  height: 200, // set fixed height for tooltip
  show: true,
  formatter: function (params) {
    const date = params.value[1].toLocaleDateString();
    const time = params.value[1].toLocaleTimeString();
    const size = params.value[2];
    const rstyle = params.value[3];
    const dstate = params.value[4];
    const dstyle = params.value[5];
    const speedLimit = params.value[6];
    const speed = params.value[7];

    // Create canvas element
    const canvas = document.createElement('canvas');
    canvas.width = 200;
    canvas.height = 160;

    // Get canvas context
    const ctx = canvas.getContext('2d');

    // Draw speed limit bar graph
    const speedLimitBarWidth = 25;
    const speedLimitBarHeight = speedLimit * canvas.height / 100;
    const speedLimitBarX = 60;
    const speedLimitBarY = canvas.height - speedLimitBarHeight;
    ctx.fillStyle = '#DC143C';
    ctx.fillRect(speedLimitBarX, speedLimitBarY, speedLimitBarWidth, speedLimitBarHeight);

    // Draw speed bar graph
    const speedBarWidth = 25;
    const speedBarHeight = speed * canvas.height / 100;
    const speedBarX = 120;
    const speedBarY = canvas.height - speedBarHeight;
    ctx.fillStyle = '#3CB371';
    ctx.fillRect(speedBarX, speedBarY, speedBarWidth, speedBarHeight);

    // Add data labels
    ctx.fillStyle = '#696463';
    ctx.font = 'bold 12px Arial';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText(speedLimit, speedLimitBarX + speedLimitBarWidth / 2, speedLimitBarY - speedLimitBarHeight / 5);
    ctx.fillText(speed, speedBarX + speedBarWidth / 2, speedBarY - speedBarHeight / 5);

    // Draw x-axis line
    ctx.strokeStyle = '#525354';
    ctx.lineWidth = 1;
    ctx.beginPath();
    ctx.moveTo(8, canvas.height);
    ctx.lineTo(canvas.width, canvas.height);
    ctx.stroke();

    // Draw y-axis line
    ctx.strokeStyle = '#525354';
    ctx.lineWidth = 0.7;
    ctx.beginPath();
    ctx.moveTo(speedLimitBarX - speedLimitBarWidth / 0.49, 0);
    ctx.lineTo(speedLimitBarX - speedLimitBarWidth / 0.49, canvas.height);
    ctx.stroke();

    // Create img element with data URL
    const img = document.createElement('img');
    img.src = canvas.toDataURL();



// Generate tooltip content
const tooltipContent =
  '<div style="text-align: left;">' +
  '<span style="display: inline-block; width: 120px;">Date: </span>' + date + '<br>' +
  '<span style="display: inline-block; width: 120px;">Time: </span>' + time + '<br>' +
  '<span style="display: inline-block; width: 120px;">Risk Value: </span>' + size + '<br>' +
  '<span style="display: inline-block; width: 120px;">Risk Style: </span>' + rstyle + '<br>' +
  '<span style="display: inline-block; width: 120px;">Driver State: </span>' + dstate + '<br>' +
  '<span style="display: inline-block; width: 120px;">Driving Style: </span>' + dstyle + '<br>' +
  img.outerHTML +
  '</div>';

return tooltipContent;
}
},
dataZoom: [{orient: 'vertical',
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
                  startValue: '0',
                  left: '20%',
                  height: '4%',
                  bottom: '1.5%',
                 },
                 {
                  type: 'inside'
                 }],
    xAxis: {
          type: 'category',
          boundaryGap: true,

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

      title: {
       text: "COUNT",
       textStyle: {
       fontSize: 14,
       fontWeight: "bold",
       color: "#403e3a",
      },
    top: 55,
    right: 18,
  },
  visualMap: {
      // show: false,
      top: 85,
      right: 25,
      seriesIndex: 1,
      pieces: [
        {
          min:3,
          max:3,
          color:"#f44336",
          label:  "" + data.filter(item => item[0] === 'Sudden Braking').length
        },
        {
          min:2,
          max:2,
          color: "#2196f3",
          label:  "" + data.filter(item => item[0] === 'Over Speed').length
        },
        {
          min:1,
          max:1,
          color: "#ffeb3b",
          label:  "" + data.filter(item => item[0] === 'Curve').length
        },
        {
          min:0,
          max:0,
          color: "#7bb57d",
          label:  "" + data.filter(item => item[0] === 'Force Acceleration').length
        },
      ],
      outOfRange: {
        color: "#999",
      },
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
               
                "Sudden Braking",
                "Over Speed",
                "Curve",
                "Force Acceleration",
                "Pedestrian Crossing",
                "School Zone",
                "Stop Sign",
                "Priority",
                "Animal Crossing",
                "Caution",
                "Hill",
                "Hill DownWards",
                "Hill UpwnWards",
                "Icy Conditions",
                "Intersection",
                "Lane Merge",
                "Low Gear Area",
                "Mobile use",
                "Narrow Road",
                "No OverTaking",
                "Railway Crossing",
                "Risk Of Grounding",
                "Slippery Roads",
                "Traffic Light",
                "Wind",
                "Winding Road",
                "Yield",
              ];

              const colors = [
                
               
              "#f44336", 
              "#2196f3", 
              "#ffeb3b", 
              "#7bb57d",
              "#8b00ff",
              "#db67a6",
              "#f0b74f",
              "#ffc0cb",
              "#9bbdac",
              "#807c7c",
              "#ad8b7b",
              "#8c488c",
              "#91910d",
              "#079494",
              "#993f3f",
              "#ffa07a",
              "#5e5eb5",
              "#c9c479",
              "#cd5c5c",
              "#b299c4",
              "#808080",
              "#a16ca1",
              "#783434",
              "#e6853c",
              "#008080",
              "#714287",
              "#adbd37"


              ];
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
  