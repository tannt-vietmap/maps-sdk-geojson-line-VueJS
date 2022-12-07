
<template>
  <div id="map"></div>
</template>

<script>
import vietmapgl from "../assets/sdk";

export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      data: null,
    };
  },
  methods: {
    addTileMap() {
      //display tile layer
      this.map = new vietmapgl.Map({
        container: "map",
        style:
          "https://maps.vietmap.vn/mt/tm/style.json?apikey=YOUR_API_KEY", // stylesheet location
        center: [106.68189581514225,10.764994908339784], // starting position [lng, lat]
        zoom: 14,
        pitch: 90, // starting zoom
      });
    },
    addGeojsonLine() {
      var app = this;
      this.map.on("load", function () {
        app.map.addSource("route", {
          type: "geojson",
          data: {
            type: "Feature",
            properties: {},
            geometry: {
              type: "LineString",
              coordinates: [
                [106.7061597962484, 10.770688562901288],
                [106.69057544335796, 10.768747133937572],
                [106.68189581514225, 10.764994908339784],
                [106.67440708752872, 10.757690582434833],
                [106.65985878585263, 10.7548236124389],
              ],
            },
          },
        });
        app.map.addLayer({
          id: "route",
          type: "line",
          source: "route",
          layout: {
            "line-join": "round",
            "line-cap": "round",
          },
          paint: {
            "line-color": "red",
            "line-width": 8,
          },
        });
      });
    },
  },
  mounted() {
    this.addTileMap();
    this.addGeojsonLine();
  },
};
</script>
 
<style>
#map {
  width: 100%;
  height: 100%;
}
</style>
