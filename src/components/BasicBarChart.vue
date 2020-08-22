<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-01 12:11:07
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-22 10:49:15
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
            type: 'bar',
            barWidth: 16,
            data: [320, 332, 301, 334, 390],
          },
          {
            name: '数据2',
            type: 'bar',
            barWidth: 16,
            data: [220, 182, 300, 234, 190],
          },
          {
            name: '数据3',
            type: 'bar',
            barWidth: 16,
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
        console.error('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(item => item.name)
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
          top: '35%',
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
          // 轴
          axisLine: {
            show: true,
            lineStyle: {
              // color: '#52FB6B',
            },
          },
          // 轴标注
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
          // 轴分割线
          splitLine: {
            show: true,
            lineStyle: {
              // color: '#52FB6B',
              type: 'solid',
            },
          },
        },
        yAxis: {
          name: '个',
          type: 'value',
          // 轴
          axisLine: {
            show: true,
            lineStyle: {
              // color: '#52FB6B',
            },
          },
          // 轴标注
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
          // 轴分割线
          splitLine: {
            show: true,
            lineStyle: {
              // color: '#52FB6B',
              type: 'solid',
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