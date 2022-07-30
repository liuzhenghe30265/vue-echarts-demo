<template>
  <div
    ref="chart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
import 'echarts-liquidfill'
export default {
  name: 'chart',
  props: {
    value: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  data () {
    return {
      chart: null,
      chartData: {
        name: '总量',
        text: '200',
        data: 0.5
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
      const chartDOM = this.$refs.chart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData = this.value
        this.chart = echarts.init(this.$refs.chart)
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
    // 图表配置
    chartOption () {
      return {
        title: {
          text: this.chartData.text,
          textStyle: {
            fontWeight: 'bold',
            fontSize: 28,
            color: '#00DDFF',
            fontFamily: 'Arial'
          },
          x: 'center',
          y: '50%'
        },
        graphic: [
          {
            type: 'group',
            left: 'center',
            top: '40%',
            children: [
              {
                type: 'text',
                z: 100,
                left: '10',
                top: 'middle',
                style: {
                  fill: '#AED8E5',
                  text: this.chartData.name,
                  fontSize: 14
                }
              }
            ]
          }
        ],
        series: [
          {
            type: 'liquidFill',
            radius: '60%',
            center: ['50%', '55%'],
            //   shape: 'roundRect',
            data: [
              {
                value: this.chartData.data,
                itemStyle: {
                  color: {
                    type: 'linear',
                    x: 0,
                    y: 0,
                    x2: 0,
                    y2: 1,
                    colorStops: [
                      {
                        offset: 1,
                        color: '#52FB6B'
                      },
                      {
                        offset: 0,
                        color: '#A152FB'
                      }
                    ],
                    globalCoord: false
                  }
                }
              }
            ],
            backgroundStyle: {
              color: 'transparent'
            },
            outline: {
              borderDistance: 3,
              itemStyle: {
                borderWidth: 2,
                borderColor: '#A152FB'
              }
            },
            label: {
              normal: {
                formatter: ''
              }
            }
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