<template>
  <div class="charts-container">
    <ul>
      <li>
        <basic-line-chart>
        </basic-line-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicLineChart.vue">🔗</a>
      </li>
      <li>
        <basic-bar-chart>
        </basic-bar-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicBarChart.vue">🔗</a>
      </li>
      <li>
        <double-bar-chart>
        </double-bar-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/DoubleBarChart.vue">🔗</a>
      </li>
      <li>
        <basic-pie-chart>
        </basic-pie-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicPieChart.vue">🔗</a>
      </li>
      <li>
        <liquidfill-chart>
        </liquidfill-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LiquidfillChart.vue">🔗</a>
      </li>
      <li>
        <progressbar-chart>
        </progressbar-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/ProgressbarChart.vue">🔗</a>
      </li>
      <li>
        <pictorial-bar-chart>
        </pictorial-bar-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/PictorialBarChart.vue">🔗</a>
      </li>
      <li>
        <customized-radar-chart>
        </customized-radar-chart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/CustomizedRadarChart.vue">🔗</a>
      </li>
      <div class="clear"></div>
    </ul>
  </div>
</template>

<script>
/* eslint-disable vue/no-unused-components */
import CustomizedRadarChart from '@/components/CustomizedRadarChart.vue'
import PictorialBarChart from '@/components/PictorialBarChart.vue'
import ProgressbarChart from '@/components/ProgressbarChart.vue'
import LiquidfillChart from '@/components/LiquidfillChart.vue'
import BasicPieChart from '@/components/BasicPieChart.vue'
import DoubleBarChart from '@/components/DoubleBarChart.vue'
import BasicBarChart from '@/components/BasicBarChart.vue'
import BasicLineChart from '@/components/BasicLineChart.vue'
export default {
  name: 'Home',
  components: {
    CustomizedRadarChart,
    PictorialBarChart,
    ProgressbarChart,
    LiquidfillChart,
    BasicPieChart,
    DoubleBarChart,
    BasicBarChart,
    BasicLineChart
  },
  data() {
    return {
      color: ['#52FB6B', '#A152FB', '#52BDFB', '#FBED52', '#FB5252']
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
      width: 25%;
      float: left;
      box-sizing: border-box;
      padding: 0 10px;
      margin-bottom: 20px;
      .chart {
        width: 100%;
        height: 240px;
      }
      a {
        font-size: 18px;
        color: #409eff;
        font-weight: bold;
        display: block;
        margin-bottom: 10px;
        line-height: 20px;
      }
    }
  }
}
@media screen and (max-width: 1200px) {
  .charts-container {
    ul {
      li {
        width: 33.3%;
      }
    }
  }
}

@media screen and (max-width: 1002px) {
  .charts-container {
    ul {
      li {
        width: 50%;
      }
    }
  }
}

@media screen and (max-width: 758px) {
  .charts-container {
    ul {
      li {
        width: 100%;
      }
    }
  }
}
</style>