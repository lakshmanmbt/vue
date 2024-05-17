<template>
  <div>
    <div ref="chart" style="height: 400px;"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  mounted() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      const chart = echarts.init(this.$refs.chart);

      const data = [
        [ // Ride 1
          10, 10, 10, 10 // Scores for driving score, anticipation, driving skill, self-confidence
        ],
        [ // Ride 1
          2, 9, 10, 5 // Scores for driving score, anticipation, driving skill, self-confidence
        ],
      ];

      const scores = ['Driving Score', 'Anticipation', 'Driving Skill', 'Self Confidence'];

      const option = {
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow',
          },
          formatter: (params) => {
            let data = '';

            data += `<strong>${params[0].name}</strong><br/>`;

            params.forEach((item) => {
              data += `
                <span style="display:inline-block;margin-right:5px;border-radius:10px;width:10px;height:10px;background-color:${item.color}"></span>
                ${item.seriesName}: ${item.value}
                <br/>
              `;
            });

            return data;
          },
        },
        legend: {
          data: scores,
        },
        xAxis: {
          type: "category",
          axisTick: { show: false },
          axisLabel: {
          show: true,
          rotate: 90,
          fontSize: 13,
        },
          data: data.map((_, index) => `Ride ${index + 1}`),
        },
        yAxis: {
          type: "value",
          min: 0,
          max: 100,
          interval: 10,
        },
        series: scores.map((score, index) => ({
        name: score,
        type: 'bar',
        stack: 'stack',
        data: data.map((ride) => ({
          value: ride[index],
          stack: index.toString(), // Use the index as the stack name
          label: {
              show: true,
              position: 'insideTop',
              formatter: '{c}', // Display the value of each data point
            },
        })),
      })),

      };

      chart.setOption(option);
    },
  },
};
</script>
