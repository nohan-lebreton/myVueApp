<script setup>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'

import { onMounted, ref, computed, watchEffect } from "vue";
import {useRouter} from 'vue-router'
const router = useRouter()

const props = defineProps(['page'])

const events = ref("");
const totalEvents = ref(0)

const page = computed(() => props.page)

const hasNextPage = computed(()=>{
  const totalPages = Math.ceil(totalEvents.value /2)
  return page.value < totalPages
})

onMounted(() => {
  watchEffect(()=>{
    events.value = null
    EventService.getEvents(2, page.value)
      .then((response) => {
        events.value = response.data;
        totalEvents.value = response.headers['x-total-count']
      })
      .catch((error) => {
        router.push({
        name: 'network-error'
    })
      });
  })
});
</script>

<template>
  <h1>Events for Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />

    <router-link
      :to="{ name: 'event-list', query: { page: page - 1 } }"
      rel="prev"
      v-if="page != 1"
      >Prev Page</router-link
    >

    <router-link
      :to="{ name: 'event-list', query: { page: page + 1 } }"
      rel="next"
      v-if="hasNextPage"
      >Next Page</router-link
    >
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>

