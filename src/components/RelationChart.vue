<template>
  <div
    ref="chart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'RelationChart',
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
      chart: null
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
      return {
        animationDurationUpdate: 3000,
        animationEasingUpdate: 'quinticInOut',
        label: {
          normal: {
            show: true,
            textStyle: {
              fontSize: 12
            }
          }
        },
        legend: {
          x: 'center',
          show: true,
          data: ['关系1', '关系2', '关系3']
        },
        series: [
          {
            type: 'graph',
            layout: 'force',
            symbolSize: 45,
            focusNodeAdjacency: true,
            roam: false,
            categories: [{
              name: '关系1',
              itemStyle: {
                normal: {
                  color: '#52FB6B'
                }
              }
            }, {
              name: '关系2',
              itemStyle: {
                normal: {
                  color: '#A152FB'
                }
              }
            }, {
              name: '关系3',
              itemStyle: {
                normal: {
                  color: '#52BDFB'
                }
              }
            }],
            label: {
              normal: {
                show: true,
                textStyle: {
                  fontSize: 12
                }
              }
            },
            force: {
              repulsion: 1000
            },
            edgeSymbolSize: [4, 50],
            edgeLabel: {
              normal: {
                show: true,
                textStyle: {
                  fontSize: 10
                },
                formatter: '{c}'
              }
            },
            data: [{
              name: '腰椎间盘突出症',
              draggable: true
            }, {
              name: '椎间盘突出',
              category: 1,
              draggable: true
            }, {
              name: '腰椎管狭窄',
              category: 1,
              draggable: true
            }, {
              name: '腰椎滑脱',
              category: 1,
              draggable: true
            }, {
              name: '腰部疼痛',
              category: 1,
              draggable: true
            }, {
              name: '下肢疼痛',
              category: 2,
              draggable: true
            }, {
              name: '腰部钝痛',
              category: 2,
              draggable: true
            }, {
              name: '腰部钝痛，平躺时缓解',
              category: 2,
              draggable: true
            }, {
              name: '男性',
              category: 2,
              draggable: true
            }, {
              name: '女性',
              category: 3,
              draggable: true
            }, {
              name: '45岁到60岁',
              category: 4,
              draggable: true
            }, {
              name: '0岁到14岁',
              category: 5,
              draggable: true
            }],
            links: [{
              source: 0,
              target: 1,
              category: 0,
              value: '关系1'
            }, {
              source: 0,
              target: 2,
              value: '关系1'
            }, {
              source: 0,
              target: 3,
              value: '关系1'
            }, {
              source: 0,
              target: 4,
              value: '关系1'
            }, {
              source: 1,
              target: 2,
              value: '关系1'
            }, {
              source: 0,
              target: 5,
              value: '关系2'
            }, {
              source: 4,
              target: 5,
              value: '关系2'
            }, {
              source: 2,
              target: 8,
              value: '关系2'
            }, {
              source: 0,
              target: 12,
              value: '关系2'
            }, {
              source: 6,
              target: 11,
              value: '关系2'
            }, {
              source: 6,
              target: 3,
              value: '关系3'
            }, {
              source: 7,
              target: 5,
              value: '关系3'
            }, {
              source: 9,
              target: 10,
              value: '关系3'
            }, {
              source: 3,
              target: 10,
              value: '关系3'
            }, {
              source: 2,
              target: 11,
              value: '关系3'
            }],
            lineStyle: {
              normal: {
                opacity: 0.9,
                width: 1,
                curveness: 0
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
