<template>
  <div
    ref="chart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'Chart',
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
      chartData: {
        data: [
          {
            name: '百度',
            value: 100
          },
          {
            name: '搜狗',
            value: 200
          },
          {
            name: '谷歌',
            value: 300
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
      const chartDOM = this.$refs.chart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // 处理数据
        // this.chartData.data = this.value // 使用父组件传递的数据
        const valArr = this.chartData.data.map(item => item.value)
        this.chartData.total = eval(valArr.join('+'))
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
    // 图表配置
    chartOption () {
      const _this = this
      return {
        animation: true,
        // 提示工具
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {c} ({d}%)',
          // 固定提示窗口
          position: (point, params, dom, rect, size) => {
            // return { left: 0, top: 0 }
            // return [point[0], '10%']
            // return [0, point[1]]
            // return [point[1], 0]
          }
        },
        // 图例
        legend: {
          show: true,
          orient: 'vertical',
          icon: 'rect', // circle, rect, line, roundRect, triangle, diamond, pin, arrow, none
          top: 'middle',
          left: 'middle',
          itemWidth: 20,
          itemHeight: 8,
          padding: [0, 5],
          itemGap: 20,
          data: _this.chartData.data,
          // 格式化图例文字
          formatter: name => {
            const resObj = {}
            for (let i = 0; i < _this.chartData.data.length; i++) {
              resObj[_this.chartData.data[i]['name']] = _this.chartData.data[i]
            }
            const arr = [
              name,
              resObj[name].value + ',',
              ((resObj[name].value / _this.chartData.total) * 100).toFixed(2) +
              '%'
            ]
            return arr.join('')
          }
        },
        series: [
          {
            name: '来源',
            type: 'pie',
            clockWise: true, // 顺时加载
            hoverAnimation: true, // 鼠标移入变大
            radius: ['30%', '40%'], // 内外环大小
            center: ['30%', '55%'], // 位置
            color: ['#52FB6B', '#A152FB', '#52BDFB'],
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: false,
                position: 'center'
              },
              emphasis: {
                show: false,
                textStyle: {
                  fontSize: '14',
                  fontWeight: 'bold'
                }
              }
            },
            labelLine: {
              normal: {
                show: true
              }
            },
            data: this.chartData.data
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
