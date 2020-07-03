<template>
  <div class="dashboard">
    <header>
      <div class="right">
        <span class="sub">实时监控显示</span> |
        <span class="time">{{ new Date().Format("hh:mm") }}</span>
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
      <transition name="fadeRight">
        <div class="right" v-if="left">
          <div class="box">
            <div style="height: 100%" v-bar>
              <div>
                <right1></right1>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>

    <transition name="fadeUp">
      <div v-show="left" class="bottom">
        <img @click="onTest" src="../assets/bottom.png" alt="" />
      </div>
    </transition>

    <Modal v-model="detail" title="资产详情" :width="1280">
      <img src="./detail.png" style="width: 100%" alt="" />
    </Modal>
  </div>
</template>

<script>
import L from "leaflet";
import "leaflet.chinatmsproviders";
import "proj4leaflet";
import { tiledMapLayer } from "esri-leaflet";
import left1 from "./left1";
import right1 from "./right1";
export default {
  name: "Home",
  components: { left1, right1 },
  data() {
    return {
      left: false,
      detail: false
    };
  },
  methods: {
    renderMap() {
      const crs = new L.Proj.CRS(
        "EPSG:4490",
        "+proj=longlat +ellps=GRS80 +no_defs",
        {
          origin: [-180.0, 90.0],
          resolutions: [
            1.40625,
            0.703125,
            0.3515625,
            0.17578125,
            0.087890625,
            0.0439453125,
            0.02197265625,
            0.010986328125,
            0.0054931640625,
            0.00274658203125,
            0.001373291015625,
            6.866455078125e-4,
            3.4332275390625e-4,
            1.71661376953125e-4,
            8.58306884765625e-5,
            4.291534423828125e-5,
            2.1457672119140625e-5,
            1.0728836059570312e-5,
            5.364418029785156e-6,
            2.682209014892578e-6,
            1.341104507446289e-6
          ]
        }
      );
      this.map = new L.map(this.$refs.map, {
        zoom: 18,
        crs: crs,
        center: [30.775918364524838, 120.72676420211792],
        attributionControl: false,
        zoomControl: false
      });
      // L.tileLayer.chinaProvider("Google.Satellite.Map").addTo(this.map);
      const target = new tiledMapLayer({
        url:
          "https://zrzyhghj2.jiaxing.gov.cn/arcgis/rest/services/JXSKY/JXALD/MapServer"
      });
      this.map.addLayer(target);
      const ll = [
        [30.77701807022095, 120.72474718093872],
        [30.776562094688416, 120.72506904602051],
        [30.776540637016296, 120.72533190250398],
        [30.776562094688416, 120.72556257247923],
        [30.77655673027039, 120.72572886943819],
        [30.776465535163883, 120.72570741176605],
        [30.77641725540161, 120.72568058967589],
        [30.776352882385257, 120.72571814060211],
        [30.776267051696777, 120.72580933570863],
        [30.776277780532837, 120.72587370872498],
        [30.77618658542633, 120.72573959827423],
        [30.776106119155884, 120.72579324245453],
        [30.775972008705143, 120.72590053081512],
        [30.77583789825439, 120.72559475898743],
        [30.775719881057743, 120.72549283504488],
        [30.775832533836365, 120.72538018226624],
        [30.775886178016663, 120.72526216506958],
        [30.775784254074097, 120.725160241127],
        [30.775650143623356, 120.7250314950943],
        [30.775446295738224, 120.72503685951231],
        [30.775392651557922, 120.72513341903687],
        [30.775151252746582, 120.72517096996309],
        [30.77467918395996, 120.72520315647127],
        [30.774523615837097, 120.72544991970064],
        [30.774866938591003, 120.7261848449707],
        [30.775403380393982, 120.72761178016663],
        [30.775929093360897, 120.72866320610045],
        [30.77629387378693, 120.72922110557556],
        [30.777554512023926, 120.72631895542145],
        [30.77701807022095, 120.72474718093872]
      ];
      const polygon = L.polygon(ll, {
        color: "#6495ED",
        weight: 8,
        fillColor: "",
        fillOpacity: 0.00001
      });
      polygon.addTo(this.map);
      polygon.on("click", () => {
        this.modal = true;
      });
      this.drawBoundary([ll]);

      setTimeout(() => {
        this.left = true;
      }, 100);

      const latlngs = [];
      this.map.on("click", e => {
        latlngs.push([e.latlng.lat, e.latlng.lng]);
        console.log(JSON.stringify(latlngs));
      });

      this.polygon = new L.polygon(
        [
          [30.77595591545105, 120.72711288928986],
          [30.77582180500031, 120.72675883769989],
          [30.77566623687744, 120.72665691375734],
          [30.775467753410343, 120.72676956653594],
          [30.775376558303837, 120.72692513465881],
          [30.775510668754578, 120.72750449180604],
          [30.77571451663971, 120.72749912738801],
          [30.77584862709045, 120.72743475437164],
          [30.775918364524838, 120.72722017765047]
        ],
        {
          color: "#333",
          weight: 1,
          fillColor: "yellow",
          fillOpacity: 0.4
        }
      ).addTo(this.map);

      this.polygon
        .bindPopup(
          `
        <div class="f-popup">
        <div class="f-popup__header">
        <span>梅湾街03商铺</span>
        <a href="javascript:;" onclick="onDetail()">详情</a>
</div>
<div class="f-popup__content">
<table>
<tr>
<td class="name">产权号：</td>
<td class="value">00001</td>
<td class="name">租赁状态：</td>
<td class="value">已租</td>
</tr>
<tr>
<td class="name">资产地址</td>
<td class="value" colspan="3">梅湾街03商铺</td>
</tr>
<tr>
<td class="name">房屋面积：</td>
<td class="value">1200㎡</td>
<td class="name">土地面积：</td>
<td class="value">2000㎡</td>
</tr>
<tr>
<td class="name">自用面积：</td>
<td class="value">-</td>
<td class="name">外借面积：</td>
<td class="value">-</td>
</tr>
<tr>
<td class="name">空置面积：</td>
<td class="value">0</td>
<td class="name">出租面积：</td>
<td class="value">1200㎡</td>
</tr>
<tr>
<td class="name">：</td>
<td class="value" colspan="3">00001</td>
</tr>
</table>
</div>
</div>`,
          {
            keepInView: true,
            className: "f-popup",
            minWidth: 200
          }
        )
        .openPopup();
    },
    onTest() {
      this.$Message.error("开发中...");
    },
    drawBoundary(blist) {
      /*画遮蔽层的相关方法
       *思路: 首先在中国地图最外画一圈，圈住理论上所有的中国领土，然后再将每个闭合区域合并进来，并全部连到西北角。
       *      这样就做出了一个经过多次西北角的闭合多边形*/
      //定义中国东南西北端点，作为第一层
      var pNW = { lat: 59.0, lng: 73.0 };
      var pNE = { lat: 59.0, lng: 136.0 };
      var pSE = { lat: 3.0, lng: 136.0 };
      var pSW = { lat: 3.0, lng: 73.0 };
      //向数组中添加一次闭合多边形，并将西北角再加一次作为之后画闭合区域的起点
      var pArray = [];
      pArray.push(pNW);
      pArray.push(pSW);
      pArray.push(pSE);
      pArray.push(pNE);
      pArray.push(pNW);
      //循环添加各闭合区域
      for (var i = 0; i < blist.length; i++) {
        var points = [];
        blist[i].forEach(function(v) {
          points.push({ lat: v[0], lng: v[1] });
        });

        //将闭合区域加到遮蔽层上，每次添加完后要再加一次西北角作为下次添加的起点和最后一次的终点
        pArray = pArray.concat(points);
        pArray.push(pArray[0]);
      }
      //添加遮蔽层
      var plyall = L.polygon(pArray, {
        color: "transparent",
        fillColor: "#000",
        fillOpacity: 0.5
      }); //建立多边形覆盖物
      plyall.addTo(this.map);
    }
  },
  mounted() {
    this.renderMap();

    window.onDetail = () => {
      this.detail = true;
    };
  }
};
</script>
<style lang="less">
.f-popup {
  .leaflet-popup-close-button {
    top: 5px !important;
    color: #515a6e !important;
    font-size: 16px !important;
    right: 5px !important;
  }
  .leaflet-popup-tip {
  }
  .leaflet-popup-content-wrapper {
    border-radius: 5px;
    box-shadow: 0 1px 4px rgba(0, 0, 0, 0.4);
    .leaflet-popup-content {
      margin: 0;
      p {
        margin: 0;
      }

      .f-popup__loading {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        text-align: center;
        background-color: #fff;
        padding-top: 15px;
      }

      .f-popup__tabs {
        margin: 5px;
        display: flex;
        border-left: 1px solid #ddd;
        border-right: 1px solid #ddd;

        .tab {
          flex: 1;
          border-top: 1px solid #ddd;
          border-bottom: 1px solid #ddd;
          border-right: 1px solid #ddd;
          text-align: center;
          padding: 3px 0;
          cursor: pointer;
          font-size: 12px;
          background-color: #f1f1f1;
          color: #666;
          position: relative;
          &:last-child {
            border-right: none;
          }
          &.selected {
            background-color: #2d8cf0;
            color: #fff;
            border-color: #2d8cf0;
            cursor: default;
            &:after {
              content: " ";
              position: absolute;
              bottom: 100%;
              z-index: 100;
              left: 50%;
              margin-left: -6px;
              width: 0;
              height: 0;
              border-right: 6px solid transparent;
              border-left: 6px solid transparent;
              border-bottom: 6px solid #2d8cf0;
            }
          }
        }
      }

      .f-popup__header {
        background-color: #f9f9f9;
        height: 32px;
        line-height: 32px;
        border-bottom: 1px solid #ccc;
        font-weight: bold;
        color: #333;
        padding: 0 10px;
      }

      .f-popup__content {
        padding: 10px 6px;
        position: relative;
        min-height: 120px;

        table {
          border-collapse: collapse;
          width: 100%;
          td {
            border: 1px solid #ddd;
            padding: 4px;
          }
          td.time {
            color: #2d8cf0;
          }
          td.name {
            width: 80px;
            text-align: right;
            padding-right: 15px;
            background-color: #f1f1f1;
            color: #666;
          }
          td.value {
            min-width: 60px;
          }
          td.device {
            background-color: #fff;
          }
        }
      }
    }
  }
}
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
        border-radius: 4px;
      }
    }

    .right {
      .box {
        width: 400px;
        position: absolute;
        right: 0;
        bottom: 40px;
        top: 20px;
        border-top: 1px solid rgb(0, 232, 70);
        border-bottom: 1px solid rgb(0, 232, 70);
        border-left: 1px solid rgb(0, 232, 70);
        background-color: rgba(0, 0, 0, 0.4);
        border-radius: 4px;
      }
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
