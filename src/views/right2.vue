<template>
  <div class="p-right">
    <div class="item">
      <div class="item-header">
        <span>实时监控</span>
      </div>
      <div class="item-body">
        <Row :gutter="10" class="video">
          <i-col :span="12">
            <img src="./video/1.png" alt="" />
          </i-col>
          <i-col :span="12"> <img src="./video/2.png" alt=""/></i-col>
          <i-col :span="12"> <img src="./video/3.png" alt=""/></i-col>
          <i-col :span="12"> <img src="./video/4.png" alt=""/></i-col>
          <i-col :span="12"> <img src="./video/5.png" alt=""/></i-col>
          <i-col :span="12"> <img src="./video/6.png" alt=""/></i-col>
        </Row>
      </div>
    </div>
    <div class="item">
      <div class="item-header">
        <span>设备统计</span>
      </div>
      <div class="item-body">
        <div class="chart" ref="c1"></div>
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
      if (this.chart) return;
      this.chart = echarts.init(this.$refs.c1);
      const xData = ["门禁", "道闸", "摄像头", "电子图", "警报"];
      const y1Data = [30, 20, 10, 22, 45];
      const option = {
        backgroundColor: "",
        grid: {
          left: "10%",
          right: "5%",
          top: "15%",
          bottom: "10%"
        },
        title: {
          show: false
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        legend: {
          data: ["报警统计"],
          align: "auto",
          itemWidth: 11,
          itemHeight: 11,
          textStyle: {
            color: "#ffffff",
            fontSize: 14
          }
        },
        toolbox: {
          show: false
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              //---坐标轴 刻度
              show: true //---是否显示
            },
            axisLine: {
              //---坐标轴 轴线
              show: true, //---是否显示
              lineStyle: {
                color: "rgba(255,255,255,.1)",
                width: 1,
                type: "dotted"
              }
            },

            axisLabel: {
              //X轴文字
              textStyle: {
                fontSize: 12,

                color: "#fff"
              }
            },
            data: xData
          }
        ],
        yAxis: [
          {
            type: "value",
            splitLine: {
              //分割线
              show: true,
              lineStyle: {
                color: "rgba(255,255,255,.2)",
                width: 1,
                type: "dotted"
              }
            },

            axisLabel: {
              //Y轴刻度值

              formatter: "{value}",

              textStyle: {
                fontSize: 12,

                color: "#fff"
              }
            },

            axisLine: {
              //---坐标轴 轴线

              show: false //---是否显示
            }
          }
        ],
        series: [
          {
            name: "报警统计",
            type: "bar",
            label: {
              // normal: {
              //     show: true,
              //     position: 'top',
              //     textStyle: {
              //         color: '#1dacfe'
              //     }
              // }
            },
            itemStyle: {
              normal: {
                barBorderRadius: [30, 30, 0, 0],
                color: new echarts.graphic.LinearGradient(
                  0,
                  1,
                  0,
                  0,
                  [
                    {
                      offset: 0,
                      color: "#15b3ff" // 0% 处的颜色
                    },
                    {
                      offset: 1,
                      color: "#a2e2ff" // 100% 处的颜色
                    }
                  ],
                  false
                )
              }
            },
            barWidth: "30%",
            yAxisIndex: 0,
            data: y1Data
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
      .video {
        img {
          width: 100%;
          margin-bottom: 4px;
          cursor: pointer;
        }
      }
      .chart {
        height: 240px;
      }
    }
  }
}
</style>
