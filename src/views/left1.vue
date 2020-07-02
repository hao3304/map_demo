<template>
  <div class="p-left">
    <div class="item">
      <div class="item-header">
        <span>资产总览</span>
      </div>
      <div class="item-body">
        <table class="t1">
          <tr>
            <td>总面积：</td>
            <td><span>110000</span>m³</td>
          </tr>
          <tr>
            <td>总价值：</td>
            <td><span>4.8</span>亿</td>
          </tr>
          <tr>
            <td>总资产数量：</td>
            <td><span>176</span>间</td>
          </tr>
          <tr>
            <td>总出租面积：</td>
            <td><span>80000</span>m³</td>
          </tr>
          <tr>
            <td>总空置面积：</td>
            <td><span>7600</span>m³</td>
          </tr>
          <tr>
            <td>总出租率：</td>
            <td><span>91</span>%</td>
          </tr>
        </table>
      </div>
    </div>

    <div class="item">
      <div class="item-header">
        <span>设备资产</span>
      </div>
      <div class="item-body">
        <table class="t2">
          <tr>
            <td>
              <img src="./zc/界面-恢复的_11.png" alt="" />
            </td>
            <td class="value">683/989</td>
            <td>
              <img src="./zc/界面-恢复的_14.png" alt="" />
            </td>
            <td class="value">683/989</td>
          </tr>
          <tr>
            <td>
              <img src="./zc/界面-恢复的_18.png" alt="" />
            </td>
            <td class="value">683/989</td>
            <td>
              <img src="./zc/界面-恢复的_19.png" alt="" />
            </td>
            <td class="value">683/989</td>
          </tr>
          <tr>
            <td>
              <img src="./zc/界面-恢复的_22.png" alt="" />
            </td>
            <td class="value">683/989</td>
            <td>
              <img src="./zc/界面-恢复的_23.png" alt="" />
            </td>
            <td class="value">683/989</td>
          </tr>
        </table>
      </div>
    </div>
    <div class="item">
      <div class="item-header">
        <span>水电缴纳情况</span>
      </div>
      <div class="item-body">
        <div class="chart" ref="c1" style="height: 172px"></div>
      </div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "left1",
  methods: {
    renderChart() {
      if (!this.chart) {
        this.chart = echarts.init(this.$refs.c1);
      }
      const option = {
        color: ["#595a0d", "#00E947", "#bbb"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow"
          }
        },
        legend: {
          data: ["水费", "电费", "物业费"],
          textStyle: {
            color: "#fff"
          }
        },
        grid: {
          bottom: 30,
          top: 40
        },
        xAxis: [
          {
            type: "category",
            axisTick: { show: false },
            data: ["2016", "2017", "2018", "2019"],
            axisLabel: {
              color: "#fff"
            }
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: "#fff"
            }
          }
        ],
        series: [
          {
            name: "水费",
            type: "bar",
            barGap: 0,

            data: [301, 334, 390, 223]
          },
          {
            name: "电费",
            type: "bar",

            data: [191, 234, 290, 234]
          },
          {
            name: "物业费",
            type: "bar",

            data: [201, 154, 190, 187]
          }
        ]
      };

      this.chart.setOption(option);
    }
  },
  mounted() {
    this.renderChart();
  }
};
</script>

<style lang="less" scoped>
.p-left {
  padding: 0 20px;
  .item {
    margin-top: 20px;
    .item-header {
      height: 34px;
      padding: 0 10px;

      span {
        color: #333;
        display: inline-block;
        text-align: center;
        background-image: url("./item-header.png");
        background-repeat: no-repeat;
        background-size: 150px 100%;
        line-height: 34px;
        font-size: 16px;
        width: 150px;
        height: 100%;
      }
    }
    .item-body {
      padding: 10px 0;
      table {
        width: 240px;
        margin: 0 auto;
        border-collapse: collapse;
        &.t1 {
          td {
            color: rgb(1, 233, 71);
            font-size: 14px;
            border-bottom: 1px dashed #bbb;
            padding: 4px 0;
            span {
              color: #fff;
              font-size: 16px;
            }
          }
        }

        &.t2 {
          td {
            padding: 8px;
            img {
              width: 56px;
            }
            color: #fff;
            font-size: 16px;
          }
        }
      }
    }
  }
}
</style>
