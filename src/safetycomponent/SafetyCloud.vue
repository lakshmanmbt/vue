<template>
  <div id="scatter-chart" style="width: 200%; height: 800px;"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  mounted() {
    const scatterChart = echarts.init(document.getElementById('scatter-chart'));

    const scatterData = [
      [3, 20],
      [4, 70],
      [12, 40],
      [10, 80],
      [80, 10],
      [90, 90],
      [100, 20],
      [40, 100],
      [1, 0],
      [50, 50.0001],
      [10.0, 10.200],
      [9.030, 99.999],
    ];

    const option = {
      grid: {
        left: '10%',
        right: '66%',
        bottom: '10%',
        top: '10%',
        containLabel: true,
        aspectRatio: 1,
      },
      xAxis: {
        type: 'value',
        name: 'SAFE     MODERATE                                                                                  RISKY                                                                                                ',
        nameLocation: 'center',
        nameTextStyle: {
            fontSize: 10,
            color: '#000'
           },
        nameGap: 25, // adjust the gap between title and axis line
        offset:0,
        min: 0,
        max: 100,
        splitNumber: 100,
        axisLabel: {
          show: true,
          color: '#262626',
          formatter: function (value) {
                if ([0, 6, 16 ].includes(value)) 
                   {return value;} 
                else if ([99].includes(value)){
                  {return value+1;} 
                }
                else {return '';}
         },

        },
        axisTick: {
          show: false,
        },
        axisLine: {
            show:false,
            lineStyle: {color: '#bfbfbf',width: 1}
          },
          splitLine: {
          show: true,
          lineStyle: {
            color: ['#000000', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', '#000000', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', '#000000', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent','transparent','#000000'],
            opacity: 1,
            type: "solid",
          },
        },
        
      },
      yAxis: {
        type: 'value',
        name: 'LOW AUDACITY                                                                              HIGH AUDACITY',
        nameLocation: 'center',
        nameTextStyle: {
            fontSize: 10,
            color: '#000'
           },
        nameGap: 25, // adjust the gap between title and axis line
        offset:0,
        min: 0,
        max: 100,
        splitNumber: 100,
        axisLabel: {
          show: true,
          color: '#262626',
          formatter: function (value) {
                if ([0,50, 100].includes(value)) {
                   return value;
              } else {
                   return '';
              }
         },

        },
        axisTick: {
          show: false,
        },
        axisLine: {
            show:false,
            lineStyle: {color: '#bfbfbf',width: 1}
          },
          splitLine: {
            lineStyle: {
            color: ['#000000', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', '#000000', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent'
            , 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent', 'transparent','#000000'],
            opacity: 1,
            type: "solid",
          },
        },
      },
      legend: {
              data: ['Good Driver', 'Sportive Driver','Quiet Safe Driver', 'Reckless Driver',  'Quiet Dangerous Driver', 'Dangerous Driver'],
              orient: 'horizontal',
              left: 230,
              top: 'top',
              textStyle: {color: '#262626'}                   
              },
      tooltip: {
    formatter: function (params) {
    const x = params.data[0];
    const y = params.data[1];
    let type = '';
    
    if (x >= 0 && x <= 6 && y >= 0 && y <= 50) 
      {type = 'Good Driver';}
    else if (x > 6 && x <= 16 && y >= 0 && y <= 50) 
      {type = 'Quiet Safe Driver';}
    else if (x > 16 && x <= 100 && y >= 0 && y <= 50) 
      {type = 'Quiet Dangerous Driver';}
    else if (x >= 0 && x <= 6 && y > 50 && y <= 100) 
      {type = 'Sportive Driver';}
    else if (x > 6 && x <= 16 && y > 50 && y <= 100) 
      {type = 'Reckless Driver';}
    else if (x > 16 && x <= 100 && y > 50 && y <= 100) 
      {type = 'Dangerous Driver';}
    
    return '<div style="text-align:left">' +
      '<b><u>' + type + '</u></b>' +
      '<br>Anticipatory Driving: ' + x +
      '<br>Self Confidence: ' + y +
      '</div>';
  }
},
  series: [
    {
      type: 'scatter',
      name: 'Good Driver',
      data: scatterData.filter((d) => d[0] >= 0 && d[0] <= 6 && d[1] >= 0 && d[1] <= 50),
      symbolSize: 10,
      symbol: 'circle',
      itemStyle: {
        color: '#346140',
      },
    },
    {
      type: 'scatter',
      name: 'Sportive Driver',
      data: scatterData.filter((d) => d[0] >= 0 && d[0] <= 6 && d[1] > 50 && d[1] <= 100),
      symbolSize: 10,
      symbol: 'square',
      itemStyle: {
        color: '#6da67c',
      },
    },
    {
      type: 'scatter',
      name: 'Quiet Safe Driver',
      data: scatterData.filter((d) => d[0] > 6 && d[0] <= 16 && d[1] >= 0 && d[1] <= 50),
      symbolSize: 12,
      symbol: 'triangle',
      itemStyle: {
        color: '#E9B506',
      },
    },
    {
      type: 'scatter',
      name: 'Reckless Driver',
      data: scatterData.filter((d) => d[0] > 6 && d[0] <= 16 && d[1] > 50 && d[1] <= 100),
      symbolSize: 10,
      symbol: 'emptytriangle',
      itemStyle: {
        color: '#F6D259',
      },
    },
    {
      type: 'scatter',
      name: 'Quiet Dangerous Driver',
      data: scatterData.filter((d) => d[0] > 16 && d[0] <= 100 && d[1] >= 0 && d[1] <= 50),
      symbolSize: 10,
      symbol: 'emptysquare',
      itemStyle: {
        color: '#FF0505',
      },
    },  
    {
      type: 'scatter',
      name: 'Dangerous Driver',
      data: scatterData.filter((d) => d[0] > 16 && d[0] <= 100 && d[1] > 50 && d[1] <= 100),
      symbolSize: 10,
      symbol: 'emptycircle',
      itemStyle: {
        color: '#AF0505',
      },
    },
  ],
  // graphic: [
  //       {
  //         type: 'polygon',
  //         bounding: 'raw',
  //         shape: {
  //           points: [
  //             [297, 80.5],
  //             [297, 700],
  //             [957.5, 700],
  //             [957.5, 80.5],
  //           ],
  //         },
  //         style: {
  //           fill: {
  //             type: 'linear',
  //             x: 0.01,
  //             y: 1,
  //             x2: 1,
  //             y2: 0.9,
  //             colorStops: [
  //                { offset: 0, color: 'rgba(146, 208, 80, 0.9)' },      // Green
  //                 { offset: 0.1, color: 'rgba(255, 255, 255, 1)' }, // White
  //                 { offset: 0.3, color: 'rgba(255, 59, 59, 0.5)' },       // Red
  //                 { offset: 0.35, color: 'rgba(255, 59, 59, 0.54)' },       // Red
  //                 { offset: 0.4, color: 'rgba(255, 59, 59, 0.58)' },       // Red/
  //                 { offset: 0.45, color: 'rgba(255, 59, 59, 0.62)' },       // Red
  //                 { offset: 0.5, color: 'rgba(255, 59, 59, 0.66)' },       // Red
  //                 { offset: 0.55, color: 'rgba(255, 59, 59, 0.7)' },       // Red
  //                 { offset: 0.6, color: 'rgba(255, 59, 59, 0.74)' },       // Red
  //                 { offset: 0.65, color: 'rgba(255, 59, 59, 0.78)' },       // Red
  //                 { offset: 0.7, color: 'rgba(255, 59, 59, 0.82)' },       // Red
  //                 { offset: 0.75, color: 'rgba(255, 59, 59, 0.86)' },       // Red
  //                 { offset: 0.8, color: 'rgba(255, 59, 59, 0.9)' },       // Red
  //                 { offset: 0.85, color: 'rgba(255, 59, 59, 0.94)' },       // Red
  //                 { offset: 0.9, color: 'rgba(255, 59, 59, 0.98)' },       // Red
  //                 { offset: 0.95, color: 'rgba(255, 59, 59, 0.99)' },       // Red
  //                 { offset: 1, color: 'rgba(255, 59, 59, 1)' },       // Red
  //                         ],
  //           },
  //         },
  //       },
  //     ],
    };

    scatterChart.setOption(option);
  },
};
</script>

<style scoped>
#scatter-chart {
  height: 500px;
}
</style>
