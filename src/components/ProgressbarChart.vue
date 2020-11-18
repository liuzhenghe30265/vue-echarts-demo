<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-07-30 15:10:39
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-11-10 16:42:13
 * @Descripttion: 进度条效果
--> 
<template>
  <div ref="ProgressbarChart"
       class="chart"></div>
</template>
<script>
import echarts from 'echarts'
import bg from '@/assets/bgi.png'
export default {
  name: 'ProgressbarChart',
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
          { name: '进度1', count: 100 },
          { name: '进度2', count: 200 },
          { name: '进度3', count: 300 },
          { name: '进度4', count: 200 },
          { name: '进度5', count: 100 },
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
      let chartDOM = this.$refs.ProgressbarChart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(_ => _.name)
        this.chartData.count = this.chartData.data.map(_ => _.count)
        this.chartData.max = Math.max(...this.chartData.count)
        this.chartData.pictorialBar = this.chartData.data.map(
          (d, index, arr) => {
            return {
              name: d.name,
              value: +this.chartData.max + 20,
              symbol: `image://${bg}`,
            }
          }
        )
        let chart = echarts.init(this.$refs.ProgressbarChart)
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
    // 图表配置
    chartOption() {
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
          top: '0%',
          right: '0%',
          bottom: '0%',
          left: '0%',
          containLabel: true,
        },
        xAxis: [
          {
            type: 'value',
            position: 'bottom',
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: false,
              color: '#01ACE0',
              interval: 0,
              fontSize: 12,
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
            type: 'category',
            data: this.chartData.name,
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: true,
              interval: 0,
              margin: 10,
              color: '#00B9EF',
              fontSize: '12',
              // 文字对齐方式
              textStyle: {
                align: 'right',
                baseline: 'middle',
              },
              // formatter: function (value) {
              //   return '{' + value + '| }\n{value|' + value + '}';
              // },
              // rich: {
              //   value: {
              //     lineHeight: 30,
              //     align: 'center'
              //   },
              //   Sunny: {
              //     height: 40,
              //     align: 'center',
              //     backgroundColor: {
              //       // image: weatherIcons.Sunny
              //     }
              //   },
              //   Cloudy: {
              //     height: 40,
              //     align: 'center',
              //     backgroundColor: {
              //       // image: weatherIcons.Cloudy
              //     }
              //   },
              //   Showers: {
              //     height: 40,
              //     align: 'center',
              //     backgroundColor: {
              //       // image: weatherIcons.Showers
              //     }
              //   }
              // }
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333',
              },
            },
          },
          {
            type: 'category',
            data: this.chartData.count,
            axisTick: {
              show: false,
            },
            axisLabel: {
              color: '#00DDFF',
              fontSize: '12',
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#333',
              },
            },
          },
        ],
        series: [
          {
            name: '',
            type: 'bar',
            barWidth: '40%',
            barGap: '-80%',
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
                      color: '#00B8FF',
                    },
                    {
                      offset: 1,
                      color: '#04BBA2',
                    },
                  ],
                },
                barBorderRadius: [20, 20, 20, 20],
              },
            },
            z: 10,
            animationDuration: 3000,
            animationEasing: 'elasticOut',
            animationDelay: function (dataIndex, params) {
              return dataIndex * 300
            },
            data: this.chartData.count,
          },
          {
            name: '',
            type: 'pictorialBar',
            barWidth: '80%',
            barGap: '-100%',
            z: 5,
            symbolRepeat: false,
            symbolSize: ['100%', '100%'],
            // itemStyle: {
            //   normal: {
            //     opacity: '0.1',
            //     color: 'rgba(0,185,239,0.30)',
            //     barBorderRadius: [20, 20, 20, 20],
            //     borderColor: 'rgba(21,92,218,0.30)',
            //     borderWidth: 1
            //   }
            // },
            animationDuration: 3000,
            animationEasing: 'elasticOut',
            animationDelay: function (dataIndex, params) {
              return dataIndex * 300
            },
            data: this.chartData.pictorialBar,
          },
        ],
      }
    },
  },
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
