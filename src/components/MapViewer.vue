<template>
  <div ref="mapRef" id="map_container"></div>
</template>
<script setup lang="ts">
import L, { type ColorGradientConfig, type HeatLayer } from 'leaflet'
import 'leaflet.heat'
import 'leaflet/dist/leaflet.css'
import { computed, onMounted, ref, watch, type PropType } from 'vue'
import type { LocationArray } from '../types'

const theme_map: Record<string, ColorGradientConfig> = {
  deep_sea: {
    0.0: 'rgb(0, 0, 0)',
    0.6: 'rgb(24, 53, 103)',
    0.75: 'rgb(46, 100, 158)',
    0.9: 'rgb(23, 173, 203)',
    1.0: 'rgb(0, 250, 250)'
  },
  aqua_white: {
    0: 'black',
    0.5: 'aqua',
    1: 'white'
  }
}

const mapRef = ref<HTMLElement | null>(null)
const props = defineProps({
  locations: Object as PropType<LocationArray>,
  radius: Number,
  minOpacity: Number,
  theme: String
})

let map: L.Map | null = null
let heatLayer: HeatLayer | null = null

onMounted(() => {
  if (mapRef.value !== null) {
    map = L.map(mapRef.value, {
      center: [23.611, 120.768],
      zoom: 3
    })

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map)

    heatLayer = L.heatLayer(heatLatLngTuple.value, heatMapOption.value).addTo(map)
  }
})

const heatLatLngTuple = computed(
  () => props.locations?.map((loc) => [loc.lat, loc.lng, 0.5] as L.HeatLatLngTuple) ?? []
)

const heatMapOption = computed<L.HeatMapOptions>(() => ({
  radius: props.radius,
  minOpacity: props.minOpacity,
  gradient: props.theme ? theme_map[props.theme] : undefined
}))

watch(heatLatLngTuple, () => {
  if (heatLayer !== null) {
    heatLayer.setLatLngs(heatLatLngTuple.value)
  }
})

watch(heatMapOption, () => {
  if (heatLayer !== null) {
    heatLayer.setOptions(heatMapOption.value)
  }
})
</script>
<style scoped>
#map_container {
  position: fixed;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
}
</style>
