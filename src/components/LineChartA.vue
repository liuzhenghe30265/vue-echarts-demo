<!--
 * @Author: liuzhenghe
 * @Email: liuzhenghe@allinmd.cn
 * @Date: 2021-01-21 14:31:53
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2021-02-06 10:27:55
 * @Descripttion: 
-->

<template>
  <div
    ref="LineChartA"
    class="chart">
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'LineChartA',
  props: {
    value: {
      type: Array,
      default() {
        return []
      },
    },
  },
  watch: {
    value: {
      immediate: true,
      handler: function (val) {
        this.drawChart()
      }
    },
  },
  data() {
    return {
      chartData: {
        data: [
          {
            name: '数据1',
            type: 'line',
            smooth: true,
            icon: 'rect',
            data: [820, 932, 901, 934, 1290, 1330, 1320],
          },
          {
            name: '数据2',
            type: 'line',
            smooth: true,
            // icon: 'rect',
            data: [100, 200, 300, 400, 400, 500, 600],
          },
        ],
      },
    }
  },
  mounted() {
    this.drawChart()
  },
  methods: {
    // 绘制图表
    drawChart() {
      let chartDOM = this.$refs.LineChartA
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(item => item.name)
        let chart = echarts.init(this.$refs.LineChartA)
        chart.clear()
        chart.setOption(this.chartOption())
        let work = null
        window.addEventListener('resize', () => {
          if (work == null) {
            work = setTimeout(() => {
              chart.resize()
              work = null
            }, 100)
          }
        })
      }
    },
    // 绘制图表
    chartOption() {
      return {
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#6a7985'
            }
          }
        },
        animation: true,
        legend: {
          data: ['data1', 'data2'],
          icon: 'roundRect',
          itemHeight: 9,
          itemWidth: 48,
          textStyle: {
            color: ' #333',
            fontSize: 16,
          },
        },
        color: ['#52FB6B', '#A152FB', '#52BDFB'],
        grid: {
          top: '35%',
          left: '5%',
          right: '5%',
          bottom: '10%',
          containLabel: true,
        },
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
          splitLine: {
            show: false,
            lineStyle: {
              color: '#333',
              type: 'dashed',
            },
          },
        },
        yAxis: {
          type: 'value',
          name: '个',
          nameTextStyle: {
            color: '#333',
            fontSize: 12,
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: '#999',
              type: 'dashed',
            },
          },
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
        },
        series: [{
          data: [120, 200, 150, 80, 70, 110, 130],
          name: 'data1',
          smooth: true,
          type: 'line',
          symbol: 'roundRect',
          symbolSize: [10, 20],
          lineStyle: {
            color: '#52FB6B',
            width: 4,
            type: 'solid'
          },
          itemStyle: {
            borderWidth: 1,
            borderColor: '#fff',
            color: '#52FB6B'
          }
        },
        {
          data: [104, 205, 157, 180, 170, 160, 180],
          name: 'data2',
          smooth: true,
          type: 'line',
          symbol: 'roundRect',
          symbolSize: [10, 20],
          lineStyle: {
            color: '#A152FB',
            width: 4,
            type: 'solid'
          },
          itemStyle: {
            borderWidth: 1,
            borderColor: '#fff',
            color: '#A152FB'
          }
        }],
      }
    },
  },
}
</script>

<style scoped>
.chart {
  width: 100%;
  height: 100%;
  text-align: center;
  margin: 0 auto;
}
</style>