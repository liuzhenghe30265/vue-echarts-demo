<template>
  <div class="charts-container">
    <ul>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BaseBarChart.vue">基础柱状图</a>
        <base-bar-chart>
        </base-bar-chart>
      </li>
      <li>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/PieChart.vue">基础饼图</a>
        <base-pie-chart>
        </base-pie-chart>
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
import BasePieChart from '@/components/BasePieChart.vue'
import LiquidfillChart from '@/components/LiquidfillChart.vue'
import ProgressbarChart from '@/components/ProgressbarChart.vue'
import BaseBarChart from '@/components/BaseBarChart.vue'

export default {
  name: 'Home',
  components: {
    BaseBarChart,
    ProgressbarChart,
    LiquidfillChart,
    BasePieChart,
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