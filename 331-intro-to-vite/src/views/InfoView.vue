<script setup lang="ts">
import InfoCard from '@/components/InfoCard.vue'
import type { Event, Student } from '@/types'
import { ref, onMounted } from 'vue'
import InfoService from '@/services/InfoService'

const events = ref<Student[]>()

onMounted(() => {
  InfoService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <h1>Events For Good</h1>
    <!-- new element -->
  <div class="events">
    <InfoCard v-for="event in events" :key="event.id" :student="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>