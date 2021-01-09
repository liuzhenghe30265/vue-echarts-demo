<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-01 12:11:07
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-22 11:07:43
 * @Descripttion: 象形柱状图
--> 
<template>
  <div ref="PictorialBarChart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'PictorialBarChart',
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
  mounted() {
    this.drawChart()
    setInterval(() => {
      this.drawChart()
    }, 5000)
  },
  created() { },
  methods: {
    // 绘制图表
    drawChart() {
      let chartDOM = this.$refs.PictorialBarChart
      if (!chartDOM) {
        console.warn('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(item => item.name)
        this.chartData.count = this.chartData.data.map(item => item.count)
        let chart = echarts.init(this.$refs.PictorialBarChart)
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
            data: name,
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
            data: name,
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