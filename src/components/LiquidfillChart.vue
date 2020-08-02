<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-07-28 09:55:52
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-02 10:21:07
 * @Descripttion: 水球
--> 
<template>
  <div ref="LiquidfillChart"
    class="chart"></div>
</template>

<script>
import echarts from 'echarts'
import 'echarts-liquidfill'
export default {
  name: 'LiquidfillChart',
  components: {},
  data() {
    return {
      chartData: {
        name: '总量',
        text: '200',
        data: 0.5,
      },
    }
  },
  watch: {
    // chartData: {
    //   handler: (val, oldVal) => {
    //     this.drawChart()
    //   },
    //   deep: true,
    // },
  },
  props: {
    // chartData: {
    //   type: Array,
    //   default() {
    //     return []
    //   },
    // },
  },
  mounted() {
    this.drawChart()
  },
  methods: {
    // 绘制图表
    drawChart() {
      let chartDOM = this.$refs.LiquidfillChart
      if (!chartDOM) {
        console.error(`echarts init dom failed`)
        return false
      } else {
        let chart = echarts.init(this.$refs.LiquidfillChart)
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
      const _this = this
      return {
        title: {
          text: this.chartData.text,
          textStyle: {
            fontWeight: 'bold',
            fontSize: 28,
            color: '#00DDFF',
            fontFamily: 'Arial',
          },
          x: 'center',
          y: '50%',
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
                  fontSize: 14,
                },
              },
            ],
          },
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
                        color: '#52FB6B',
                      },
                      {
                        offset: 0,
                        color: '#A152FB',
                      },
                    ],
                    globalCoord: false,
                  },
                },
              },
            ],
            backgroundStyle: {
              color: 'transparent',
            },
            outline: {
              borderDistance: 3,
              itemStyle: {
                borderWidth: 2,
                borderColor: '#A152FB',
              },
            },
            label: {
              normal: {
                formatter: '',
              },
            },
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