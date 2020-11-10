<!--
 * @Author: liuzhenghe
 * @Email: 15901450207@163.com
 * @Date: 2020-07-26 09:32:45
 * @LastEditors: liuzhenghe
 * @LastEditTime: 2020-08-22 10:58:52
 * @Descripttion: 基础饼图
--> 
<template>
  <div ref="BasicPieChart"
       class="chart">
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'BasicPieChart',
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
            name: '百度',
            value: 100,
          },
          {
            name: '搜狗',
            value: 200,
          },
          {
            name: '谷歌',
            value: 300,
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
      let chartDOM = this.$refs.BasicPieChart
      if (!chartDOM) {
        console.error('echarts init dom failed')
        return false
      } else {
        // 处理数据
        // this.chartData.data = this.value
        let valArr = this.chartData.data.map(item => item.value)
        this.chartData.total = eval(valArr.join('+'))
        let chart = echarts.init(this.$refs.BasicPieChart)
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
        animation: true,
        // 提示工具
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {c} ({d}%)',
        },
        // 图例
        legend: {
          show: true,
          orient: 'vertical',
          icon: 'rect',
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
              '%',
            ]
            return arr.join('')
          },
        },
        series: [
          {
            name: '来源',
            type: 'pie',
            clockWise: true, // 顺时加载
            hoverAnimation: true, // 鼠标移入变大
            radius: ['50%', '60%'],
            // center: ['30%', '55%'],
            color: ['#52FB6B', '#A152FB', '#52BDFB'],
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: false,
                position: 'center',
              },
              emphasis: {
                show: false,
                textStyle: {
                  fontSize: '14',
                  fontWeight: 'bold',
                },
              },
            },
            labelLine: {
              normal: {
                show: true,
              },
            },
            data: this.chartData.data,
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