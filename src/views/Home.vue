<template>
  <div class="charts-container">
    <ul>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicBarChart.vue">基础柱状图</a>
        <basic-bar-chart>
        </basic-bar-chart>
      </li>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicPieChart.vue">基础饼图</a>
        <basic-pie-chart>
        </basic-pie-chart>
      </li>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LiquidfillChart.vue">水球</a>
        <liquidfill-chart>
        </liquidfill-chart>
      </li>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/ProgressbarChart.vue">进度条</a>
        <progressbar-chart>
        </progressbar-chart>
      </li>
      <div class="clear"></div>
    </ul>
  </div>
</template>

<script>
import BasicBarChart from '@/components/BasicBarChart.vue'
import BasicPieChart from '@/components/BasicPieChart.vue'
import LiquidfillChart from '@/components/LiquidfillChart.vue'
import ProgressbarChart from '@/components/ProgressbarChart.vue'

export default {
  name: 'Home',
  components: {
    BasicPieChart,
    BasicBarChart,
    ProgressbarChart,
    LiquidfillChart,
  },
  data() {
    return {
      color: ['#52FB6B', '#A152FB', '#52BDFB', '#FBED52', '#FB5252'],
    }
  },
}
</script>
<style lang="scss" scoped>
.clear {
  width: 100%;
  height: 100%;
  clear: both;
  overflow: hidden;
}
.charts-container {
  padding: 20px;
  ul {
    overflow: hidden;
    margin: 0 -10px;
    li {
      width: 33.3%;
      float: left;
      box-sizing: border-box;
      padding: 0 10px;
      margin-bottom: 20px;
      .chart {
        width: 100%;
        height: 240px;
      }
      a {
        font-size: 24px;
        color: #409eff;
        font-weight: bold;
        display: block;
        margin-bottom: 10px;
      }
    }
  }
}
</style>