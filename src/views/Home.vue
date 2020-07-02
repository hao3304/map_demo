<template>
  <div class="dashboard">
    <header></header>
    <div class="content">
      <div class="block"></div>
      <div id="map" ref="map">
        <div class="left">
          <div class="box">
            <left1></left1>
          </div>
        </div>
        <div class="right"></div>
      </div>
    </div>
  </div>
</template>

<script>
import L from "leaflet";
import "leaflet.chinatmsproviders";
import left1 from "./left1";
export default {
  name: "Home",
  components: { left1 },
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
  }
  .content {
    flex: 1;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    #map {
      flex: 1;
      position: relative;

      .left {
        width: 600px;
        background: linear-gradient(
          to right,
          rgba(0, 0, 0, 0.8),
          rgba(0, 0, 0, 0)
        );
        position: absolute;
        top: 0;
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
        }
      }

      .right {
        width: 600px;
        background: linear-gradient(
          to left,
          rgba(0, 0, 0, 0.8),
          rgba(0, 0, 0, 0)
        );
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        z-index: 1000;
      }
    }
    .block {
      height: 64px;
    }
  }
}
</style>
