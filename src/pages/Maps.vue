<template>
  <div style="height: 700px; width: 100%">
    <l-map
      v-if="showMap"
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 80%"
      @update:center="centerUpdate"
      @update:zoom="zoomUpdate"
    >
      <l-tile-layer :url="url" :attribution="attribution" />
      <l-marker :lat-lng="withPopup">
        <l-popup>
          <div @click="innerClick">
            Smart Bin
            <p v-if="binFull">
              This bin is full
            </p>
          </div>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { latLng } from 'leaflet';
import { LMap, LTileLayer, LMarker, LPopup, LTooltip } from 'vue2-leaflet';
import io from 'socket.io-client';
let baseUrl = 'https://garbage-bin-tracker-api.herokuapp.com/';
// import UpgradeToPROVue from './UpgradeToPRO.vue';
// let socket = io.connect('http://localhost:2000');
let socket = io.connect(baseUrl);

export default {
  name: 'Example',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    // LTooltip,
  },
  data() {
    return {
      zoom: 15,
      center: latLng(4.150243659987948, 9.229274697197832),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      withPopup: latLng(4.150243659987948, 9.229274697197832),
      // withTooltip: latLng(4.15, 9.22),
      currentZoom: 11.5,
      // currentCenter: latLng(47.41322, -1.219482),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 0.5,
      },
      showMap: true,
      binFull: false,
    };
  },
  created() {
    socket.on('binFull', (data) => {
      console.log(data, 'receiving notifications from socket');
      console.log(this.binFull, 'From maps.vue');
      this.binFull = true;
    });
  },
  methods: {
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert('Click!');
    },
  },
};
</script>
