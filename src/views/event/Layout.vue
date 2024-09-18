<template>
    <div v-if="event">
        <h1>{{event.title}}</h1>
        <div id="nav">
          <router-link :to="{ name: 'event-details' }"
            >Details</router-link
          >
          |
          <router-link :to="{ name: 'event-register' }"
            >Register</router-link
          >
          |
          <router-link :to="{ name: 'event-edit' }"
            >Edit</router-link
          >
        </div>
        <router-view :event="event"></router-view>
    </div>
</template>

<script setup>
import EventService from '@/services/EventService.js'
import {ref, onMounted} from 'vue'
import {useRouter} from 'vue-router'
const router = useRouter()


const props = defineProps({
  id: {
    required: true,
  },
})
const event = ref(null)

onMounted(()=>{
  EventService.getEvent(props.id)
  .then((response)=>{
    event.value = response.data
  })
  .catch((error)=> {
    router.push({
        name: '404-resource',
        params: { resource: 'event'}
    })
  })
})
</script>

<style>

</style>