<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-13 16:40:29
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-22 11:10:08
 * @Descripttion: 自定义雷达图
-->
<template>
  <div ref="CustomizedRadarChart"
       class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'CustomizedRadarChart',
  props: {
    value: {
      type: Array,
      default() {
        return []
      },
    },
  },
  watch: {
    value: function (newV, oldV) {
      this.drawChart()
    },
  },
  data() {
    return {
      chartData: {
        data: [
          {
            name: '数据1',
            value: [100, 200],
          },
          {
            name: '数据2',
            value: [400, 500],
          },
          {
            name: '数据3',
            value: [700, 800],
          },
          {
            name: '数据4',
            value: [1000, 1100],
          },
          {
            name: '数据5',
            value: [100, 200],
          },
        ],
      },
    }
  },
  mounted() {
    this.drawChart()
  },
  created() {},
  methods: {
    // 绘制图表
    drawChart() {
      let chartDOM = this.$refs.CustomizedRadarChart
      if (!chartDOM) {
        console.error('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        let chart = echarts.init(this.$refs.CustomizedRadarChart)
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
      let _this = this
      return {
        title: {
          show: false,
        },
        tooltip: {
          trigger: 'none',
          confine: true,
        },
        legend: {
          show: false,
          orient: 'vertical',
          selectedMode: false,
          top: 'center',
          right: '5%',
          textStyle: {
            color: 'rgba(255,255,255,.6)',
            fontSize: 12,
          },
        },
        radar: {
          name: {
            color: '#AED8E5',
            // backgroundColor: {
            //   image: require('@/assets/bgi.png')
            // },
            rich: {
              a0: {
                color: '#0A1228',
                backgroundColor: '#52FB6B',
                fontSize: 14,
                padding: 5,
                fontWeight: 'bold',
                align: 'left',
              },
              a1: {
                color: '#0A1228',
                backgroundColor: '#A152FB',
                fontSize: 14,
                padding: 5,
                fontWeight: 'bold',
                align: 'left',
              },
              a2: {
                color: '#0A1228',
                backgroundColor: '#52BDFB',
                fontSize: 14,
                padding: 5,
                fontWeight: 'bold',
                align: 'left',
              },
              a3: {
                color: '#0A1228',
                backgroundColor: '#FB5252',
                fontSize: 14,
                padding: 5,
                fontWeight: 'bold',
                align: 'left',
              },
              a4: {
                color: '#0A1228',
                backgroundColor: '#FB5252',
                fontSize: 14,
                padding: 5,
                fontWeight: 'bold',
                align: 'left',
              },
              b: {
                color: '#AED8E5',
                fontWeight: 'bold',
                fontSize: 12,
                padding: [5, 0],
                align: 'left',
              },
            },
          },
          nameGap: 5,
          radius: '70%',
          center: ['50%', '55%'],
          // 数据名称（需要放到 name 中）
          indicator: this.chartData.data,
          splitArea: {
            show: true,
            areaStyle: {
              color: ['rgba(8,38,61,0.30)', 'rgba(8,38,61,0.30)'],
            },
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(0,70,124,.6)',
              type: 'dashed',
            },
          },
          splitLine: {
            lineStyle: {
              color: 'rgba(0,70,124,.6)',
              type: 'dashed',
            },
          },
        },
        series: [
          {
            type: 'radar',
            data: this.chartData.data,
            label: {
              show: false,
              color: '#727BFF',
            },
            symbol: 'circle',
            symbolSize: 8,
            itemStyle: {
              color: '#FCEC2E',
            },
            lineStyle: {
              color: {
                type: 'linear',
                x: 0, // 右
                y: 0, // 下
                x2: 1, // 左
                y2: 1, // 上
                colorStops: [
                  {
                    offset: 0,
                    color: '#FCEC2E',
                  },
                  {
                    offset: 1,
                    color: '#00DDFF',
                  },
                ],
                globalCoord: false,
              },
            },
            areaStyle: {
              show: true,
              color: {
                type: 'linear',
                x: 0, // 右
                y: 0, // 下
                x2: 1, // 左
                y2: 1, // 上
                colorStops: [
                  {
                    offset: 0,
                    color: 'rgba(252,236,46,.2)',
                  },
                  {
                    offset: 0.5,
                    color: 'transparent',
                  },
                  {
                    offset: 1,
                    color: 'rgba(0,221,255,.1)',
                  },
                ],
                globalCoord: false,
              },
            },
            animationDuration: 3000,
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