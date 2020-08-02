<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-01 12:11:07
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-02 10:14:24
 * @Descripttion: 基础柱状图
--> 
<template>
  <div ref="BasicBarChart"
    class="chart" />
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'BasicBarChart',
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
        data: [
          {
            name: '北京',
            type: 'bar',
            data: [320, 332, 301, 334, 390],
          },
          {
            name: '上海',
            type: 'bar',
            data: [220, 182, 300, 234, 190],
          },
          {
            name: '广州',
            type: 'bar',
            data: [150, 232, 100, 154, 190],
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
      let chartDOM = this.$refs.BasicBarChart
      if (!chartDOM) {
        console.error(`echarts init dom failed`)
        return false
      } else {
        this.chartData.name = this.chartData.data.map((item) => item.name)
        let chart = echarts.init(this.$refs.BasicBarChart)
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
          text: '数量统计',
          subtext: '小标题',
          left: 'left',
        },
        legend: {
          data: this.chartData.name,
          right: 0,
        },
        grid: {
          top: '25%',
          left: '5%',
          right: '5%',
          bottom: '10%',
          containLabel: true,
        },
        barGap: 0, // 间距
        color: ['#52FB6B', '#A152FB', '#52BDFB'],
        xAxis: {
          type: 'category',
          data: ['1月', '2月', '3月'],
          //   x 轴文字颜色
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
        },
        yAxis: {
          type: 'value',
          //   y 轴文字颜色
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
          //   y 轴坐标线
          splitLine: {
            lineStyle: {
              color: '#333',
              type: 'dashed',
            },
          },
        },
        series: this.chartData.data,
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