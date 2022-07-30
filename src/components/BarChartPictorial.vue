<template>
  <div
    ref="chart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'chart',
  props: {
    value: {
      type: Array,
      default () {
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
  data () {
    return {
      chart: null,
      chartData: {
        data: [
          {
            name: 'data1',
            count: 864,
          },
          {
            name: 'data2',
            count: 533,
          },
          {
            name: 'data3',
            count: 645,
          },
          {
            name: 'data4',
            count: 234,
          },
          {
            name: 'data5',
            count: 234,
          },
        ],
      },
    }
  },
  mounted () {
    this.drawChart()
  },
  destroyed () {
    echarts.dispose(this.chart)
  },
  methods: {
    // 绘制图表
    drawChart () {
      let chartDOM = this.$refs.chart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(item => item.name)
        this.chartData.count = this.chartData.data.map(item => item.count)
        this.chart = echarts.init(this.$refs.chart)
        this.chart.clear()
        this.chart.setOption(this.chartOption())
        let work = null
        window.addEventListener('resize', () => {
          if (work == null) {
            work = setTimeout(() => {
              this.chart.resize()
              work = null
            }, 100)
          }
        })
      }
    },
    // 绘制图表
    chartOption () {
      return {
        title: {
          show: false,
          text: '',
          top: '5',
          left: '10',
          textStyle: {
            fontSize: '16',
            fontWeight: 'normal',
            color: '#fff',
          },
        },
        tooltip: {
          show: false,
          trigger: 'axis',
          axisPointer: {
            type: 'line',
          },
        },
        grid: {
          top: '20%',
          bottom: '20%',
          left: '0',
          right: '5%',
          containLabel: true,
        },
        xAxis: [
          {
            type: 'category',
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: true,
              color: '#AED8E5',
              interval: 0,
              fontSize: 12,
              margin: 30,
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333',
              },
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: ['#333'],
              },
            },
          },
        ],
        yAxis: [
          {
            show: false,
            type: 'value',
            axisTick: {
              show: false,
            },
            axisLabel: {
              interval: 0,
              color: ' #00B9EF',
              fontSize: '12',
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333',
              },
            },
            splitLine: {
              show: false,
            },
          },
        ],
        series: [
          {
            name: '',
            type: 'pictorialBar',
            symbolSize: [20, 10],
            symbolOffset: [0, -6],
            symbolPosition: 'end',
            z: 12,
            label: {
              normal: {
                show: true,
                position: 'top',
                fontSize: 14,
                fontWeight: 'bold',
                color: '#FCEC2E',
              },
            },
            color: '#2DB1EF',
            data: this.chartData.count,
          },
          {
            name: '',
            type: 'pictorialBar',
            symbolSize: [20, 10],
            symbolOffset: [0, 7],
            z: 12,
            color: '#2DB1EF',
            data: this.chartData.count,
          },
          {
            name: '',
            type: 'pictorialBar',
            symbolSize: [30, 15],
            symbolOffset: [0, 12],
            z: 10,
            itemStyle: {
              normal: {
                color: 'transparent',
                borderColor: '#2EA9E5',
                borderType: 'solid',
                borderWidth: 1,
              },
            },
            data: this.chartData.count,
          },
          {
            name: '',
            type: 'pictorialBar',
            symbolSize: [50, 20],
            symbolOffset: [0, 18],
            z: 10,
            itemStyle: {
              normal: {
                color: 'transparent',
                borderColor: '#19465D',
                borderType: 'solid',
                borderWidth: 2,
              },
            },
            data: this.chartData.count,
          },
          {
            name: '',
            type: 'bar',
            barWidth: '20',
            itemStyle: {
              color: {
                type: 'liner',
                x: 0,
                y: 0,
                x2: 0,
                y2: 0.7,
                colorStops: [
                  {
                    offset: 0,
                    color: 'rgba(56,178,230,.8)',
                  },
                  {
                    offset: 1,
                    color: 'rgba(56,178,230, .1)',
                  },
                ],
              },
            },
            animationDuration: 3000,
            animationEasing: 'elasticOut',
            animationDelay: function (dataIndex, params) {
              return dataIndex * 300
            },
            data: this.chartData.count,
          },
        ],
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