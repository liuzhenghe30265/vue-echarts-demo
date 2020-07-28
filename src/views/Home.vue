<template>
  <div class="charts-container">
    <ul>
      <li>
        <a
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/src/components/PieChart.vue">基础饼图</a>
        <pie-chart></pie-chart>
      </li>
      <li>
        <a href="">水球</a>
        <liquidfill-chart>
        </liquidfill-chart>
      </li>
    </ul>
  </div>
</template>

<script>
import PieChart from '@/components/PieChart.vue'
import LiquidfillChart from '@/components/LiquidfillChart.vue' // 水球

export default {
  name: 'Home',
  components: {
    LiquidfillChart,
    PieChart,
  },
  data() {
    return {
      color: ['#52FB6B', '#A152FB', '#52BDFB', '#FBED52', '#FB5252'],
    }
  },
}
</script>
<style lang="scss" scoped>
.charts-container {
  padding: 20px;
  ul {
    overflow: hidden;
    margin: 0 -10px;
    li {
      width: 33.3%;
      height: 200px;
      float: left;
      box-sizing: border-box;
      padding: 10px;
      a {
        font-size: 24px;
        color: #409eff;
        font-weight: bold;
      }
    }
  }
}
</style>