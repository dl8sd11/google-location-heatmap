<script setup lang="ts">
import MapViewer from '@/components/MapViewer.vue'
import RecordLoader from '@/components/RecordLoader.vue'
import type { LocationArray } from '@/types'
import { ref } from 'vue'

const locationsRef = ref<LocationArray>([])

const locationReady = (locations: LocationArray) => {
  console.log('ready', locations)
  locationsRef.value = locations
}

const theme = ref('deep_sea')

const radius = ref(15)
const minOpacity = ref(0.3)
</script>
<template>
  <MapViewer :locations="locationsRef" :radius="radius" :min-opacity="minOpacity" :theme="theme" />
  <div id="menu">
    <VSlider v-model="radius" :min="1" :max="30" label="Radius" />
    <VSlider v-model="minOpacity" :min="0" :max="1" label="Min opacity" />
    <VSelect v-model="theme" label="Heat map theme" :items="['deep_sea', 'aqua_white']"></VSelect>
    <RecordLoader @on-location-ready="locationReady" />
  </div>
</template>
<style scoped>
#menu {
  background-color: white;
  padding: 10px;
  border-radius: 3px;
  position: fixed;
  right: 10px;
  bottom: 10px;
  width: 300px;
}
</style>
