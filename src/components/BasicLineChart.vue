<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-08-01 12:11:07
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-22 10:45:35
 * @Descripttion: 基础折线图
--> 
<template>
  <div ref="BasicLineChart"
       class="chart"></div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'BasicLineChart',
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
            type: 'line',
            smooth: true,
            icon: 'rect',
            data: [820, 932, 901, 934, 1290, 1330, 1320],
          },
          {
            name: '数据2',
            type: 'line',
            smooth: true,
            // icon: 'rect',
            data: [100, 200, 300, 400, 400, 500, 600],
          },
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
      let chartDOM = this.$refs.BasicLineChart
      if (!chartDOM) {
        console.error('echarts init dom failed')
        return false
      } else {
        // this.chartData.data = this.value
        this.chartData.name = this.chartData.data.map(item => item.name)
        let chart = echarts.init(this.$refs.BasicLineChart)
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
        animation: true,
        title: {
          text: '数量统计',
          subtext: '小标题',
          left: 'left',
        },
        legend: {
          // itemHeight: 2,
          // itemWidth: 14,
          data: this.chartData.data,
          textStyle: {
            color: ' #222',
            fontSize: 12,
          },
        },
        color: ['#52FB6B', '#A152FB', '#52BDFB'],
        grid: {
          top: '35%',
          left: '5%',
          right: '5%',
          bottom: '10%',
          containLabel: true,
        },
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
            },
          },
          splitLine: {
            show: false,
            lineStyle: {
              color: '#333',
              type: 'dashed',
            },
          },
        },
        yAxis: {
          type: 'value',
          name: '个',
          nameTextStyle: {
            color: '#333',
            fontSize: 12,
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: '#999',
              type: 'dashed',
            },
          },
          axisLabel: {
            textStyle: {
              color: '#333',
              fontSize: 12,
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