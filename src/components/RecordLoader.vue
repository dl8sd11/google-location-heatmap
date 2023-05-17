<template>
  <div>
    <VFileInput
      ref="fileRef"
      label="Upload Record.json"
      prepend-icon=""
      @update:model-value="onRecordChange"
    />
    <v-overlay :model-value="loading" persistent class="align-center justify-center">
      <v-progress-circular color="primary" indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </div>
</template>

<script setup lang="ts">
import type { LocationArray } from '@/types'
import { ref } from 'vue'

const emit = defineEmits<{
  (e: 'onLocationReady', locations: LocationArray): void
}>()

const fileRef = ref<HTMLInputElement | null>(null)
const loading = ref(false)

const processRecord = (record: string) => {
  const record_obj = JSON.parse(record)
  const locations = record_obj['locations'].map((record_entry: any) => {
    return {
      lat: record_entry['latitudeE7'] * 1e-7,
      lng: record_entry['longitudeE7'] * 1e-7
    }
  })
  emit('onLocationReady', locations)
}

const onRecordChange = () => {
  if (fileRef.value !== null && fileRef.value.files) {
    loading.value = true
    const reader = new FileReader()
    reader.onload = () => {
      processRecord(reader.result as string)
      loading.value = false
    }
    reader.readAsText(fileRef.value.files[0])
  }
}
</script>
