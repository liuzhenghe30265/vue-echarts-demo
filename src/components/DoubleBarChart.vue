<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-01 12:11:07
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-02 16:46:39
 * @Descripttion: 双柱状图
--> 
<template>
  <div ref="DoubleBarChart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'DoubleBarChart',
  props: {
    // data: {
    //   type: Array,
    //   default() {
    //     return []
    //   }
    // }
  },
  watch: {
    // data: {
    //   handler: function(val, oldVal) {
    //     this.drawChart()
    //   },
    //   deep: true
    // }
  },
  data() {
    return {
      chartData: {
        femal: [
          {
            age: '6岁以下',
            count: 100,
          },
          {
            age: '6-18',
            count: 120,
          },
          {
            age: '18岁以上',
            count: 200,
          },
        ],
        male: [
          {
            age: '6岁以下',
            count: 150,
          },
          {
            age: '6-18',
            count: 170,
          },
          {
            age: '18岁以上',
            count: 300,
          },
        ],
      },
    }
  },
  mounted() {
    this.drawChart()
  },
  methods: {
    // 数组排序
    sortNumber(a, b) {
      return a - b
    },
    // 绘制图表
    drawChart() {
      let chartDOM = this.$refs.DoubleBarChart
      if (!chartDOM) {
        console.error(`echarts init dom failed`)
        return false
      } else {
        this.chartData.age = this.chartData.femal.map((item) => item.age)
        this.chartData.femalCount = this.chartData.femal.map(
          (item) => item.count
        )
        this.chartData.maleCount = this.chartData.male.map((item) => item.count)
        this.chartData.age = this.chartData.femal.map((item) => item.age)
        const allCounts = this.chartData.femalCount.concat(
          this.chartData.maleCount
        )
        const maxVal = allCounts.sort(this.sortNumber).reverse()[0]
        this.chartData.maximum = Math.ceil(maxVal / 100) * 100

        let chart = echarts.init(this.$refs.DoubleBarChart)
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
        legend: {
          orient: 'horizontal',
          top: '3%',
          right: '5%',
          icon: 'roundRect',
          selectedMode: true,
          itemWidth: 16,
          itemHeight: 8,
          textStyle: {
            fontSize: 12,
            color: '#333',
          },
          data: ['女', '男'],
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow',
          },
        },
        xAxis: [
          {
            type: 'value',
            name: '人',
            splitNumber: 2,
            min: 0,
            // max: 10000,
            max: this.chartData.maximum,
            inverse: true,
            gridIndex: 0,
            axisTick: {
              show: false,
              interval: 2,
              inside: false,
            },
            axisLabel: {
              show: true,
              interval: 2,
              color: '#333',
              fontSize: 12,
            },
            axisLine: {
              show: true,
              lineStyle: {
                color: '#666',
              },
            },
            splitLine: {
              show: true,
              lineStyle: {
                color: '#333',
                opacity: 0.3,
              },
            },
          },
          {
            type: 'value',
            name: '人',
            min: 0,
            // max: 10000,
            max: this.chartData.maximum,
            splitNumber: 2,
            gridIndex: 1,
            axisTick: {
              interval: 2,
              show: false,
            }, // 是否显示刻度
            axisLine: {
              // Y轴轴线样式
              show: true, // 是否显示X轴
              lineStyle: {
                color: '#333',
              },
            },
            axisLabel: {
              show: true,
              interval: 2,
              color: '#333',
              fontSize: 12,
            },
            splitLine: {
              show: true,
              lineStyle: {
                color: '#333',
                opacity: 0.3,
              },
            },
          },
        ],
        yAxis: [
          {
            type: 'category',
            gridIndex: 0,
            inverse: true,
            // data: ['18岁以上', '6-18岁', '6岁以下'],
            data: this.chartData.age,
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: false,
            },
            axisLine: {
              show: false,
            },
          },
          {
            type: 'category',
            gridIndex: 1,
            inverse: true,
            // data: ['18岁以上', '6-18岁', '6岁以下'],
            data: this.chartData.age,
            axisTick: {
              show: false,
            },
            axisLabel: {
              interval: 0,
              color: '#A5BEC7',
              align: 'right',
              fontSize: 10,
            },
            axisLine: {
              show: false,
            },
          },
        ],
        grid: [
          {
            top: '15%',
            width: '30%',
            bottom: '15%',
            gridIndex: 0,
          },
          {
            top: '15%',
            left: '60%',
            width: '30%',
            bottom: '15%',
            gridIndex: 1,
          },
        ],
        series: [
          {
            name: '女',
            type: 'bar',
            barWidth: '30%',
            gridIndex: 0,
            itemStyle: {
              normal: {
                color: {
                  type: 'liner',
                  x: 0,
                  y: 0,
                  x2: 1,
                  y2: 0,
                  // 渐变色
                  colorStops: [
                    {
                      offset: 0,
                      color: '#52FB6B',
                    },
                    {
                      offset: 1,
                      color: '#A152FB',
                    },
                  ],
                },
                barBorderRadius: [20, 0, 0, 20],
              },
            },
            animationDuration: 3000,
            // data: [150, 250, 350],
            data: this.chartData.femalCount,
          },
          {
            name: '男',
            type: 'bar',
            barWidth: '30%',
            xAxisIndex: 1,
            yAxisIndex: 1,
            itemStyle: {
              normal: {
                color: {
                  type: 'liner',
                  x: 0,
                  y: 0,
                  x2: 1,
                  y2: 0,
                  // 渐变色
                  colorStops: [
                    {
                      offset: 0,
                      color: '#52BDFB',
                    },
                    {
                      offset: 1,
                      color: '#FBED52',
                    },
                  ],
                },
                barBorderRadius: [0, 20, 20, 0],
              },
            },
            // data: [100, 200, 300],
            data: this.chartData.maleCount,
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