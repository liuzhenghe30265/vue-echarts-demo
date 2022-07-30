<template>
  <div
    class="charts-container">
    <ul>
      <li>
        <Demo>
        </Demo>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/demo.vue">🔗</a>
      </li>
      <li>
        <RelationChart>
        </RelationChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/RelationChart.vue">🔗</a>
      </li>
      <li>
        <LineChart
          :value="chartData">
        </LineChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LineChart.vue">🔗</a>
      </li>
      <li>
        <LineChart2>
        </LineChart2>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LineChart2.vue">🔗</a>
      </li>
      <li>
        <BarChart>
        </BarChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BarChart.vue">🔗</a>
      </li>
      <li>
        <BarChartDouble>
        </BarChartDouble>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BarChartDouble.vue">🔗</a>
      </li>
      <li>
        <BarChartProcess>
        </BarChartProcess>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BarChartProcess.vue">🔗</a>
      </li>
      <li>
        <BarChartProcess2>
        </BarChartProcess2>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BarChartProcess2.vue">🔗</a>
      </li>
      <li>
        <BarChartPictorial>
        </BarChartPictorial>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BarChartPictorial.vue">🔗</a>
      </li>
      <li>
        <PieChart>
        </PieChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/PieChart.vue">🔗</a>
      </li>
      <li>
        <LiquidfillChart>
        </LiquidfillChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LiquidfillChart.vue">🔗</a>
      </li>
      <li>
        <RadarChart>
        </RadarChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/RadarChart.vue">🔗</a>
      </li>
      <li
        class="show">
        <LargeAreaChart>
        </LargeAreaChart>
        <a target="blank"
          href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LargeAreaChart.vue">🔗</a>
      </li>
      <div
        class="clear">
      </div>
    </ul>
  </div>
</template>

<script>
import Demo from '@/components/Demo.vue'
import LargeAreaChart from '@/components/LargeAreaChart.vue'
import RelationChart from '@/components/RelationChart.vue'
import LineChart2 from '@/components/LineChart2.vue'
import RadarChart from '@/components/RadarChart.vue'
import BarChartPictorial from '@/components/BarChartPictorial.vue'
import BarChartProcess from '@/components/BarChartProcess.vue'
import BarChartProcess2 from '@/components/BarChartProcess2.vue'
import LiquidfillChart from '@/components/LiquidfillChart.vue'
import PieChart from '@/components/PieChart.vue'
import BarChartDouble from '@/components/BarChartDouble.vue'
import BarChart from '@/components/BarChart.vue'
import LineChart from '@/components/LineChart.vue'
export default {
  name: 'Home',
  components: {
    Demo,
    LargeAreaChart,
    RelationChart,
    LineChart2,
    RadarChart,
    BarChartPictorial,
    BarChartProcess,
    BarChartProcess2,
    LiquidfillChart,
    PieChart,
    BarChartDouble,
    BarChart,
    LineChart,
  },
  data () {
    return {
      chartData: [
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
      width: 25%;
      float: left;
      box-sizing: border-box;
      padding: 0 10px;
      margin-bottom: 20px;
      // display: none;
      &.show {
        display: block;
      }
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