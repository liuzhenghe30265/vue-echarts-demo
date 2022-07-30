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
      timer: null,
      start: 0,
      end: 5,
      chartData: {
        data: [
          { name: '天津', count: 100, total: 200 },
          { name: '浙江', count: 200, total: 200 },
          { name: '江苏', count: 300, total: 400 },
          { name: '河北', count: 200, total: 300 },
          { name: '贵州', count: 100, total: 200 },
          { name: '山东', count: 100, total: 300 },
          { name: '山西', count: 200, total: 900 },
          { name: '北京', count: 300, total: 800 },
          { name: '上海', count: 400, total: 700 },
          { name: '广东', count: 500, total: 600 }
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
    this.play()
  },
  destroyed () {
    this.timer = null
    echarts.dispose(this.chart)
  },
  methods: {
    // 滚动播放
    play () {
      const _this = this
      if (_this.timer) {
        clearInterval(_this.timer)
      }
      _this.timer = setInterval(() => {
        if (_this.end === _this.chartData.data.length) {
          _this.start = 0
          _this.end = 5
        } else {
          _this.start = _this.start + 1
          _this.end = _this.end + 1
        }
        _this.chart.dispatchAction({
          type: 'dataZoom',
          startValue: _this.start,
          endValue: _this.end
        })
      }, 5000)
    },
    // 绘制图表
    drawChart () {
      const _this = this
      const chartDOM = this.$refs.chart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(_ => {
          return {
            value: _.name
          }
        })
        this.chartData.count = this.chartData.data.map(_ => {
          return {
            value: _.count
          }
        })
        this.chartData.total = this.chartData.data.map(_ => {
          return {
            count: _.count, // 格式化 label 时用到
            value: _.total
          }
        })
        this.chart = echarts.init(this.$refs.chart)
        this.chart.clear()
        this.chart.setOption(this.chartOption())
        this.chart.on('click', function (params) {
          console.log(params)
        })
        let work = null
        window.addEventListener('resize', () => {
          if (work === null) {
            work = setTimeout(() => {
              _this.chart.resize()
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
        title: {
          show: false,
          text: '',
          top: '5',
          left: '10',
          textStyle: {
            fontSize: '16',
            fontWeight: 'normal',
            color: '#333'
          }
        },
        tooltip: {
          show: true,
          trigger: 'axis',
          axisPointer: {
            type: 'none'
          }
        },
        grid: {
          top: '5%',
          right: '20%',
          bottom: '5%',
          left: '0%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'value',
            position: 'bottom',
            axisTick: {
              show: false
            },
            axisLabel: {
              show: false,
              color: '#01ACE0',
              interval: 0,
              fontSize: 12
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333'
              }
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: ['#333']
              }
            }
          }
        ],
        yAxis: [
          {
            type: 'category',
            data: this.chartData.name,
            axisTick: {
              show: false
            },
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
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333'
              }
            }
          },
          {
            type: 'category',
            data: this.chartData.count,
            axisTick: {
              show: false
            },
            axisLabel: {
              show: false,
              color: '#333',
              fontSize: '12'
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333'
              }
            }
          }
        ],
        // 滚动条
        // dataZoom: [
        //   {
        //     show: false,
        //     start: 0,
        //     end: 100
        //   },
        //   {
        //     type: 'inside',
        //     start: 94,
        //     end: 100
        //   },
        //   {
        //     show: true,
        //     yAxisIndex: 0,
        //     filterMode: 'empty',
        //     width: 30,
        //     height: '80%',
        //     showDataShadow: false,
        //     left: '93%'
        //   }
        // ],
        dataZoom: {
          type: 'inside',
          startValue: _this.start,
          endValue: _this.end,
          yAxisIndex: 0,
          zoomLock: true,
          zoomOnMouseWheel: true,
          moveOnMouseWheel: true,
          moveOnMouseMove: true
        },
        series: [
          {
            name: '实际运维人员',
            type: 'bar',
            barWidth: '40%',
            itemStyle: {
              normal: {
                color: {
                  type: 'liner',
                  x: 0,
                  y: 0,
                  x2: 1,
                  y2: 0,
                  colorStops: [
                    {
                      offset: 0,
                      color: '#1940FF'
                    },
                    {
                      offset: 0.5,
                      color: '#43DC9B'
                    },
                    {
                      offset: 1,
                      color: '#42FCAD'
                    }
                  ]
                },
                barBorderRadius: [0, 20, 20, 0]
              }
            },
            z: 10,
            animationDuration: 3000,
            animationEasing: 'elasticOut',
            // animationDelay: function (dataIndex) {
            //   return dataIndex * 300
            // },
            data: this.chartData.count
          },
          {
            name: '固定运维人员',
            // type: 'pictorialBar',
            // symbol: 'react',
            type: 'bar',
            stack: 'samesign',
            barWidth: '50%',
            barGap: '-110%',
            itemStyle: {
              normal: {
                color: {
                  type: 'liner',
                  x: 0,
                  y: 0,
                  x2: 1,
                  y2: 0,
                  colorStops: [
                    {
                      offset: 0,
                      color: 'rgba(0, 0, 255, 1)'
                    },
                    {
                      offset: 0.5,
                      color: 'rgba(0, 0, 255, 1)'
                    },
                    {
                      offset: 1,
                      color: 'rgba(0, 0, 255, 1)'
                    }
                  ]
                },
                borderRadius: [0, 20, 20, 0],
                barBorderRadius: [0, 20, 20, 0]
              }
            },
            z: -1,
            animationDuration: 3000,
            animationEasing: 'elasticOut',
            // animationDelay: function (dataIndex) {
            //   return dataIndex * 300
            // },
            data: this.chartData.total,
            label: {
              show: true,
              position: 'right',
              color: '#333',
              formatter: function (value) {
                if (value.data) {
                  return value.data.count + '/' + value.data.value
                }
              }
            }
          }
        ]
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.chart {
  width: 100%;
  height: 100%;
  text-align: center;
  margin: 0 auto;
}
</style>