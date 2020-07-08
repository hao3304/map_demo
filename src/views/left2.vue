<template>
  <div class="p-left">
    <div class="item">
      <div class="item-header">
        <span>安全隐患统计</span>
      </div>
      <div class="item-body">
        <h5 class="t1-header">
          <span>总数 18</span>
          <span>整顿 10</span>
        </h5>
        <Row :gutter="10">
          <i-col :span="12">
            <div class="chart" ref="c1"></div>
            <div class="star">
              <img src="../assets/star.png" alt="" />
            </div>
          </i-col>
          <i-col :span="12">
            <div class="chart" ref="c2"></div>

            <div class="star">
              <img src="../assets/star.png" v-for="n in 2" :key="n" alt="" />
            </div>
          </i-col>
          <i-col :span="12">
            <div class="chart" ref="c3"></div>
            <div class="star">
              <img
                src="../assets/star.png"
                v-for="n in 3"
                :key="n"
                alt=""
              /></div
          ></i-col>
          <i-col :span="12">
            <div class="chart" ref="c4"></div>
            <div class="star">
              <img
                src="../assets/star.png"
                v-for="n in 4"
                :key="n"
                alt=""
              /></div
          ></i-col>
        </Row>
      </div>
    </div>

    <div class="item">
      <div class="item-header">
        <span>当日游客流量</span>
      </div>
      <div class="item-body">
        <div class="t2">
          <img src="./ll/1.png" alt="" />
          <img src="./ll/2.png" alt="" />
          <img src="./ll/3.png" alt="" />
          <img src="./ll/4.png" alt="" />
        </div>
      </div>
    </div>
    <div class="item">
      <div class="item-header">
        <span>实时游客流量</span>
      </div>
      <div class="item-body">
        <div class="list">
          <div :class="{ scroll: animate }">
            <img src="./ll/5.png" v-for="item in list" :key="item" alt="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
const car = require("./ll/5.png");
export default {
  name: "left1",
  data() {
    return {
      list: [0, 1, 3],
      animate: false
    };
  },
  methods: {
    renderChart(ref, value = 8, color = "#D5ECC4") {
      const chart = echarts.init(ref);
      const option = {
        series: [
          {
            name: "泵站负载",
            type: "liquidFill",
            data: [value / 10],
            radius: "80%",
            outline: {
              itemStyle: {
                borderColor: color
              }
            },
            label: {
              fontSize: 32,
              formatter: function() {
                return value;
              }
            }
          }
        ]
      };
      chart.setOption(option);
    },
    render() {
      this.animate = true;

      setTimeout(() => {
        this.animate = false;
        const r = this.list.shift();
        this.list.push(this.list[this.list.length - 1] + 1);
        setTimeout(() => {
          this.render();
        }, 1000);
      }, 1100);
    }
  },
  mounted() {
    this.renderChart(this.$refs.c1, 4);
    this.renderChart(this.$refs.c2, 9, "#ff9900");
    this.renderChart(this.$refs.c3, 6, "yellow");
    this.renderChart(this.$refs.c4, 8, "#f5a623");
    this.render();
  }
};
</script>

<style lang="less" scoped>
.p-left {
  padding: 0 20px;
  .item {
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
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

      .t1-header {
        font-weight: normal;
        border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 0;
        span {
          border-left: 1px solid #00e947;
          margin: 0 20px;
          border-right: 1px solid #00e947;
          line-height: 16px;
          display: inline-block;
          width: 100px;
          text-align: center;
          font-size: 16px;
          color: #00e947;
        }
      }

      .star {
        display: flex;
        justify-content: center;
        margin-top: -10px;
        font-size: 0;
        padding-left: 8px;
        img {
          width: 26px;
          margin: 0 2px;
        }
      }

      .chart {
        height: 120px;
        margin-bottom: 10px;
      }

      .t2 {
        display: flex;
        margin: 5px 0;
        justify-content: space-around;
        img {
          width: 80px;
        }
      }

      .list {
        height: 152px;
        overflow: hidden;
        font-size: 0;
        .scroll {
          margin-top: -76px;
          transition: all 1s;
        }

        img {
          height: 70px;
          margin-bottom: 6px;
        }
      }
    }
  }
}
</style>
