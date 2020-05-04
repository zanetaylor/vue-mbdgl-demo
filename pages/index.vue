<template>
  <div id="map" ref="map" />
</template>

<script>
import mapboxgl from 'mapbox-gl'
import { GeoJsonLayer } from '@deck.gl/layers'
import { MapboxLayer } from '@deck.gl/mapbox'

export default {
  data () {
    return {
      accessToken: process.env.MAPBOX_TOKEN,
      mapStyle: 'mapbox://styles/zotterdas/ck9rx8iux0jje1im9egawbi58',
      latitude: 35.4832668,
      longitude: 12.9491635,
      zoom: 10,
      bearing: 0,
      pitch: 0
    }
  },
  created () {
    // creating a non reactive map object
    this.map = null;
  },
  mounted () {
    // initialize the map
    this.map = new mapboxgl.Map({
      accessToken: this.accessToken,
      container: this.$refs.map,
      style: this.mapStyle,
      center: [this.longitude, this.latitude],
      zoom: this.zoom,
      pitch: this.pitch,
      bearing: this.bearing
    })

    this.map.on('load', () => {
      this.loadLayer()
    })
  },
  methods: {
    loadLayer () {
      // create a new MapboxLayer of type GeoJSON Layer
      const layer = new MapboxLayer({
        id: 'geojson-layer',
        type: GeoJsonLayer,
        data: this.mapData,
        filled: true,
        lineWidthScale: 20,
        lineWidthMinPixels: 2,
        getFillColor: d => [245, 133, 5, 0],
        getLineColor: d => [245, 245, 245],
        getLineWidth: 1
      })
      // add the layer to map
      this.map.addLayer(layer)
    }
  }
}
</script>

<style lang="scss">
.main-content {
  width: 100vw;
  height: 100vh;
}
#map {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}
</style>
