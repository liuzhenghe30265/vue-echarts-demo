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
      }
    }
  },
  data () {
    return {
      chart: null,
      chartData: {
        data: [
          {
            date: '2020/07/01',
            data: 100
          },
          {
            date: '2020/07/02',
            data: 10
          },
          {
            date: '2020/07/03',
            data: 400
          },
          {
            date: '2020/07/04',
            data: 500
          },
          {
            date: '2020/07/05',
            data: 700
          },
          {
            date: '2020/07/06',
            data: 900
          },
          {
            date: '2020/07/07',
            data: 200
          },
          {
            date: '2020/07/08',
            data: 300
          },
          {
            date: '2020/07/09',
            data: 600
          },
          {
            date: '2020/07/10',
            data: 100
          }
        ]
      }
    }
  },
  watch: {
    value: {
      immediate: true,
      handler: function (val) {
        this.drawChart()
      }
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
      const _this = this
      const chartDOM = this.$refs.chart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.date = this.chartData.data.map(_ => {
          return {
            value: _.date
          }
        })
        this.chartData.data = this.chartData.data.map(_ => {
          return {
            value: _.data
          }
        })
        this.chart = echarts.init(this.$refs.chart)
        this.chart.clear()
        this.chart.setOption(this.chartOption())
        let work = null
        window.addEventListener('resize', () => {
          if (work === null) {
            work = setTimeout(() => {
              this.chart.resize()
              work = null
            }, 100)
          }
        })
      }
    },
    // 图表配置
    chartOption () {
      const _this = this
      return {
        tooltip: {
          trigger: 'axis',
          position: function (pt) {
            return [pt[0], '10%']
          }
        },
        grid: {
          top: '10%',
          right: '0%',
          bottom: '40%',
          left: '10%',
          containLabel: true
        },
        title: {
          left: 'center',
          text: ''
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          axisLabel: {
            show: true,
            interval: 0,
            margin: 10,
            color: '#333',
            fontSize: '12',
            textStyle: {
              align: 'right',
              baseline: 'middle'
            }
          },
          data: _this.chartData.date
        },
        yAxis: {
          type: 'value',
          boundaryGap: [0, '100%'],
          axisLabel: {
            show: false,
            interval: 0,
            margin: 10,
            color: '#333',
            fontSize: '12',
            textStyle: {
              align: 'right',
              baseline: 'middle'
            }
          }
        },
        dataZoom: [
          {
            type: 'inside',
            start: 0,
            end: 50
          },
          {
            backgroundColor: 'rgba(252, 183, 24, .2)',
            start: 0,
            end: 50
          }
        ],
        series: [
          {
            name: '总数',
            type: 'line',
            symbol: 'none',
            sampling: 'lttb',
            itemStyle: {
              color: 'rgb(252, 183, 24)'
            },
            areaStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                {
                  offset: 0,
                  color: 'rgba(252, 183, 24, 1)'
                },
                {
                  offset: 1,
                  color: 'rgba(252, 183, 24, 0)'
                }
              ])
            },
            data: _this.chartData.data
          }
        ]
      }
    }
  }
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