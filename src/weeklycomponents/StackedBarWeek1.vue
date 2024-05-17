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
        [10, 52, 200, 334, 390, 330, 220],
        [20, 82, 190, 234, 290, 330, 310],
        [30, 92, 180, 154, 190, 230, 410],
        [40, 72, 160, 114, 140, 190, 510],
        [50, 62, 140, 94, 90, 130, 610],
        [60, 52, 120, 74, 50, 90, 710],
        [70, 32, 100, 54, 10, 50, 810],
      ];

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
          data: ['A', 'B', 'C', 'D', 'E', 'F', 'G'],
        },
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
        },
        yAxis: {
          type: 'value',
        },
        series: [
          {
            name: 'A',
            type: 'bar',
            stack: 'stack',
            data: data[0],
          },
          {
            name: 'B',
            type: 'bar',
            stack: 'stack',
            data: data[1],
          },
          {
            name: 'C',
            type: 'bar',
            stack: 'stack',
            data: data[2],
          },
          {
            name: 'D',
            type: 'bar',
            stack: 'stack',
            data: data[3],
          },
          {
            name: 'E',
            type: 'bar',
            stack: 'stack',
            data: data[4],
          },
          {
            name: 'F',
            type: 'bar',
            stack: 'stack',
            data: data[5],
          },
          {
            name: 'G',
            type: 'bar',
            stack: 'stack',
            data: data[6],
          },
        ],
      };

      chart.setOption(option);
    },
  },
};
</script>