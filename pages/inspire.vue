<template>
  <div class="map-wrap">
    <div id="map" ref="map" />
    <canvas id="deck-canvas" ref="canvas" />
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
import { Deck } from '@deck.gl/core'

export default {
  data () {
    return {
      accessToken: process.env.MAPBOX_TOKEN,
      mapStyle: 'mapbox://styles/zotterdas/ck9rx8iux0jje1im9egawbi58',
      viewState: {
        latitude: 87,
        longitude: 72,
        zoom: 12,
        pitch: 0,
        bearing: 0
      }
    }
  },
  created () {
    // creating a non reactive map object
    this.map = null
    this.deck = null
  },
  mounted () {
    // initialize the map
    this.map = new mapboxgl.Map({
      accessToken: this.accessToken,
      container: this.$refs.map,
      interactive: false,
      style: this.mapStyle,
      center: [this.viewState.longitude, this.viewState.latitude],
      zoom: this.viewState.zoom,
      pitch: this.viewState.pitch,
      bearing: this.viewState.bearing
    })

    this.deck = new Deck({
      canvas: this.$refs.canvas,
      width: '100%',
      height: '100%',
      initialViewState: this.viewState,
      controller: true,
      // change the map's viewstate whenever the view state of deck.gl changes
      onViewStateChange: ({ viewState }) => {
        this.map.jumpTo({
          center: [viewState.longitude, viewState.latitude],
          zoom: viewState.zoom,
          bearing: viewState.bearing,
          pitch: viewState.pitch
        })
      }
    })
  },
  methods: {

  }
}
</script>

<style lang="scss">
.main-content,
.map-wrap {
  width: 100vw;
  height: 100vh;
  position: relative;
}
#map {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #e5e9ec;
  overflow: hidden;
}
#deck-canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
