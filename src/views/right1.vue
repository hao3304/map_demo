<template>
  <div class="p-right">
    <div class="item">
      <div class="item-header">
        <span>商户信息</span>
      </div>
      <div class="item-body">
        <table class="t1">
          <tr>
            <td>租户名称：</td>
            <td colspan="3"><span>浙商银行</span></td>
          </tr>
          <tr>
            <td>法人代表：</td>
            <td colspan="3"><span>陈某某</span></td>
          </tr>
          <tr>
            <td>联系人：</td>
            <td><span>陈某某</span></td>
            <td>电话：</td>
            <td><span>138XXXXXXXX</span></td>
          </tr>
        </table>
      </div>
    </div>
    <div class="item">
      <div class="item-body">
        <table class="t1">
          <tr>
            <td>出租开始时间：</td>
            <td><span>2018年 10月15日</span></td>
          </tr>
          <tr>
            <td>出租结束时间：</td>
            <td><span>2020年 10月15日</span></td>
          </tr>
        </table>
      </div>
    </div>
    <div class="item">
      <div class="item-header">
        <span>安全隐患</span>
      </div>
      <div class="item-body">
        <Row>
          <i-col :span="12">
            <div class="chart1" ref="c1"></div>
            <div class="chart-name">巡检隐患总数</div>
          </i-col>
          <i-col :span="12">
            <div class="chart1" ref="c2"></div>
            <div class="chart-name">已整改数</div>
          </i-col>
        </Row>
      </div>
    </div>
    <div class="item">
      <div class="item-header">
        <span>工单</span>
      </div>
      <div class="item-body">
        <div ref="c3" style="height: 200px"></div>
      </div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
import "echarts-liquidfill";
export default {
  name: "right1",
  methods: {
    renderChart() {
      if (!this.chart) {
        this.chart1 = echarts.init(this.$refs.c1);
        this.chart2 = echarts.init(this.$refs.c2);
      }
      const option = {
        series: [
          {
            name: "泵站负载",
            type: "liquidFill",
            data: [0.8],
            radius: "70%",
            outline: {
              itemStyle: {
                borderColor: "#D5ECC4"
              }
            },
            label: {
              fontSize: 32,
              formatter: function() {
                return "8";
              }
            }
          }
        ]
      };

      this.chart1.setOption(option);
      this.chart2.setOption(option);
    },
    renderChart2() {
      if (this.chart3) return;
      this.chart3 = echarts.init(this.$refs.c3);
      const option = {
        tooltip: {
          //鼠标指上时的标线
          trigger: "axis",
          axisPointer: {
            lineStyle: {
              color: "#fff"
            }
          }
        },
        legend: {
          icon: "rect",
          itemWidth: 14,
          itemHeight: 5,
          itemGap: 13,
          data: ["投诉", "已处理"],
          right: "10px",
          top: "0px",
          textStyle: {
            fontSize: 12,
            color: "#fff"
          }
        },
        grid: {
          x: 35,
          y: 25,
          x2: 15,
          y2: 25
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            axisLine: {
              lineStyle: {
                color: "#57617B"
              }
            },
            axisLabel: {
              textStyle: {
                color: "#fff"
              }
            },
            data: [
              "1月",
              "2月",
              "3月",
              "4月",
              "5月",
              "6月",
              "7月",
              "8月",
              "9月",
              "10月",
              "11月",
              "12月"
            ]
          }
        ],
        yAxis: [
          {
            type: "value",
            axisTick: {
              show: false
            },
            axisLine: {
              lineStyle: {
                color: "#57617B"
              }
            },
            axisLabel: {
              margin: 10,
              textStyle: {
                fontSize: 14,
                color: "#fff"
              }
            },
            splitLine: {
              lineStyle: {
                color: "rgba(255,255,255,.2)",
                type: "dotted"
              }
            }
          }
        ],
        series: [
          {
            name: "投诉",
            type: "line",
            smooth: true,
            lineStyle: {
              normal: {
                width: 2
              }
            },
            areaStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0,
                  0,
                  0,
                  1,
                  [
                    {
                      offset: 0,
                      color: "rgba(137, 189, 27, 0.3)"
                    },
                    {
                      offset: 0.8,
                      color: "rgba(137, 189, 27, 0)"
                    }
                  ],
                  false
                ),
                shadowColor: "rgba(0, 0, 0, 0.1)",
                shadowBlur: 10
              }
            },
            itemStyle: {
              normal: {
                color: "rgb(137,189,27)"
              }
            },
            data: [70, 65, 84, 75, 52, 61, 89, 64, 24, 52.4, 64, 73]
          },
          {
            name: "已处理",
            type: "line",
            smooth: true,
            lineStyle: {
              normal: {
                width: 2
              }
            },
            areaStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0,
                  0,
                  0,
                  1,
                  [
                    {
                      offset: 0,
                      color: "rgba(0, 136, 212, 0.3)"
                    },
                    {
                      offset: 0.8,
                      color: "rgba(0, 136, 212, 0)"
                    }
                  ],
                  false
                ),
                shadowColor: "rgba(0, 0, 0, 0.1)",
                shadowBlur: 10
              }
            },
            itemStyle: {
              normal: {
                color: "rgb(0,136,212)"
              }
            },
            data: [
              97.3,
              99.2,
              99.3,
              100.0,
              99.6,
              90.6,
              80.0,
              91.5,
              69.8,
              67.5,
              90.4,
              84.9
            ]
          }
        ]
      };
      this.chart3.setOption(option);
    }
  },
  mounted() {
    this.renderChart();
    this.renderChart2();
  }
};
</script>

<style lang="less" scoped>
.p-right {
  padding: 0 20px;
  .item {
    margin-top: 20px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
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

      .chart1 {
        height: 180px;
      }
      .chart-name {
        text-align: center;
        color: #01e947;
      }

      table {
        width: 320px;
        margin: 0 auto;
        border-collapse: collapse;
        &.t1 {
          td {
            color: rgb(1, 233, 71);
            font-size: 14px;
            padding: 4px;
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
