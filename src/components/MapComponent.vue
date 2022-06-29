<template>
  <v-container>
    <v-card>
      <div id="map"></div>
    </v-card>
  </v-container>
</template>

<script>
import "leaflet";
import "leaflet/dist/leaflet.css";
import "@ansur/leaflet-pulse-icon/dist/L.Icon.Pulse";
import "@ansur/leaflet-pulse-icon/dist/L.Icon.Pulse.css";
// import "../../node_modules/@ansur/leaflet-pulse-icon/dist/L.Icon.Pulse";
// import "@ansur/leaflet-pulse-icon/dist/L.Icon.Pulse";
// import "@ansur/leaflet-pulse-icon/dist/L.Icon.Pulse.css";

const L = window["L"];

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});

export default {
  name: "MapComponent",
  data() {
    return {
      map: null,
      layer: null,
      marker: null,
      pulseIcon: null,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = new L.Map("map", {
        center: new L.LatLng(-3.10719, -60.0261),
        zoom: 5,
      });
      this.layer = new L.tileLayer(
        "http://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}.png",
        {
          minZoom: 5,
          maxZoom: 18,
        }
      );
      this.map.addLayer(this.layer);
      this.pulseIcon = L.icon.pulse({ iconSize: [20, 20], color: "red" });
      this.marker = L.marker([50, 15], { icon: this.pulseIcon }).addTo(this.map);
    },
  },
};
</script>

<style>
#map {
  height: 600px;
}
</style>
