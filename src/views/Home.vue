<template>
  <div class="charts-container">
    <ul>
      <li class="show">
        <RelationChart>
        </RelationChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/RelationChart.vue">🔗</a>
      </li>
      <li>
        <LineChartA>
        </LineChartA>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LineChartA.vue">🔗</a>
      </li>
      <li>
        <BasicLineChart
                          :value="chartData">
        </BasicLineChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicLineChart.vue">🔗</a>
      </li>
      <li>
        <BasicBarChart>
        </BasicBarChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicBarChart.vue">🔗</a>
      </li>
      <li>
        <DoubleBarChart>
        </DoubleBarChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/DoubleBarChart.vue">🔗</a>
      </li>
      <li>
        <BasicPieChart>
        </BasicPieChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/BasicPieChart.vue">🔗</a>
      </li>
      <li>
        <LiquidfillChart>
        </LiquidfillChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/LiquidfillChart.vue">🔗</a>
      </li>
      <li>
        <ProgressbarChart>
        </ProgressbarChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/ProgressbarChart.vue">🔗</a>
      </li>
      <li>
        <PictorialBarChart>
        </PictorialBarChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/PictorialBarChart.vue">🔗</a>
      </li>
      <li>
        <CustomizedRadarChart>
        </CustomizedRadarChart>
        <a target="blank"
           href="https://github.com/liuzhenghe30265/vue-echarts-demo/blob/master/src/components/CustomizedRadarChart.vue">🔗</a>
      </li>
      <div class="clear"></div>
    </ul>
  </div>
</template>

<script>
import RelationChart from '@/components/RelationChart.vue'
import LineChartA from '@/components/LineChartA.vue'
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
    RelationChart,
    LineChartA,
    CustomizedRadarChart,
    PictorialBarChart,
    ProgressbarChart,
    LiquidfillChart,
    BasicPieChart,
    DoubleBarChart,
    BasicBarChart,
    BasicLineChart,
  },
  data() {
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