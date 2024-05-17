<template>
    <div class="bar-chart" ref="chart" style="height: 400px;"></div>
</template>
  
  <script>
  import * as echarts from 'echarts';
  
  export default {
    name: 'RiskPercentageBarChart',
    mounted() {
      this.createChart();
    },
    methods: {
      createChart() {
        const chart = echarts.init(this.$refs.chart);
  
        // Define the data directly inside the component
        const data = {
          // '0 - 10': 70,
          '10 - 20': 3,
          '20 - 30': 4,
          '30 - 40': 3,
          '40 - 50': 4,
          '50 - 60': 5,
          '60 - 70': 1,
          '70 - 80': 3.4,
          '80 - 90': 6.2,
          '90 - 100': 0.1,
        };
        const slotLabels = Object.entries(data).map(([range, count]) => `${range} (${count})`);
        // Calculate the total count combining all slots
        const totalCount = Object.values(data).reduce((sum, count) => sum + count, 0);
  
        // Calculate the percentage for each slot count
        const slotNames = Object.keys(data);
        const slotPercentages = slotNames.map((slot) => ((data[slot] / (totalCount+70)) * 100).toFixed(2));
  
        const option = {
          xAxis: {
            type: 'category',
            data: slotLabels, // Use slot names for x-axis labels
          },
          yAxis: {
            type: 'value',
            axisLabel: {
              formatter: '{value}%', // Show percentage symbol on y-axis
            },
          },
          tooltip: {
            trigger: 'axis',
            formatter: '{c0}%', // Show slot name and percentage in the tooltip
          },
          series: [
            {
              type: 'bar',
              data: slotPercentages,
            },
          ],
        };
  
        chart.setOption(option);
      },
    },
  };
  </script>
  
  <style>
  /* You can add some styling for the chart container if needed */
  .bar-chart {
    width: 100%;
  }
  </style>
  