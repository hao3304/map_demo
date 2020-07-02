<template>
  <div class="dashboard">
    <header>
      <div class="right">
        <span class="sub">实时监控显示</span> |
        <span class="time">{{ new Date().Format("hh:dd") }}</span>
        |
        <div class="date">
          <div>2020-07-03</div>
          <div>星期五</div>
        </div>
      </div>
    </header>
    <div class="content">
      <div class="block"></div>
      <div id="map" ref="map"></div>
      <transition name="fadeLeft">
        <div v-if="left" class="left">
          <div class="box">
            <div style="height: 100%" v-bar>
              <div>
                <left1></left1>
              </div>
            </div>
          </div>
        </div>
      </transition>
      <div class="right"></div>
    </div>

    <transition name="fadeUp">
      <div v-show="left" class="bottom">
        <img @click="onTest" src="../assets/bottom.png" alt="" />
      </div>
    </transition>
  </div>
</template>

<script>
import L from "leaflet";
import "leaflet.chinatmsproviders";
import left1 from "./left1";
export default {
  name: "Home",
  components: { left1 },
  data() {
    return {
      left: false
    };
  },
  methods: {
    renderMap() {
      this.map = new L.map(this.$refs.map, {
        zoom: 18,
        center: [30.75346296449824, 120.74784636497498],
        attributionControl: false,
        zoomControl: false
      });
      L.tileLayer.chinaProvider("Google.Satellite.Map").addTo(this.map);

      this.map.on("click", e => {
        console.log(e);
      });

      this.left = true;
    },
    onTest() {
      this.$Message.error("开发中...");
    }
  },
  mounted() {
    this.renderMap();
  }
};
</script>
<style lang="less">
.dashboard {
  height: 100%;
  display: flex;
  flex-direction: column;
  header {
    height: 80px;
    background-image: url("~@/assets/header.png");
    background-size: 100% 100%;
    background-repeat: no-repeat;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;

    .right {
      position: absolute;
      right: 20px;
      display: flex;
      font-size: 20px;
      color: #fff;
      height: 64px;
      align-items: center;
      .sub {
        color: #00dd4d;
        margin: 0 8px;
      }
      .time {
        font-size: 24px;
        margin: 0 8px;
      }
      .date {
        font-size: 14px;
        margin: 0 8px;
      }
    }
  }
  .content {
    flex: 1;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    #map {
      flex: 1;
      position: relative;
    }
    .left {
      width: 600px;
      background: linear-gradient(
        to right,
        rgba(0, 0, 0, 0.8),
        rgba(0, 0, 0, 0)
      );
      position: absolute;
      top: 64px;
      left: 0;
      bottom: 0;
      z-index: 1000;
      .box {
        width: 400px;
        position: absolute;
        left: 0;
        bottom: 40px;
        top: 20px;
        border-top: 1px solid rgb(0, 232, 70);
        border-right: 1px solid rgb(0, 232, 70);
        border-bottom: 1px solid rgb(0, 232, 70);
        background-color: rgba(0, 0, 0, 0.4);
      }
    }

    .right {
      width: 600px;
      top: 64px;
      background: linear-gradient(
        to left,
        rgba(0, 0, 0, 0.8),
        rgba(0, 0, 0, 0)
      );
      position: absolute;
      right: 0;
      bottom: 0;
      z-index: 1000;
    }
    .block {
      height: 64px;
    }
  }

  .bottom {
    position: absolute;
    width: 400px;
    bottom: -10px;
    left: 50%;
    z-index: 1000;
    margin-left: -200px;

    img {
      cursor: pointer;
      width: 100%;
      height: 150px;
    }
  }
}
</style>
