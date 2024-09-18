<script setup>
import {useRouter} from 'vue-router'
import { defineProps, inject } from "vue";

const { event } = defineProps(['event'])
const router = useRouter()
const GStore = inject('GStore')

const register = () => {
    GStore.flashMessage = 'You are successflully registerd for ' + event.title 
    setTimeout(()=>{
        GStore.flashMessage = ''
    }, 3000) // after 3s clear message
    //if register success push back to the event details
    router.push({
        name:'event-details'    
    })
}
</script>  

<template>
        <p>Register for the event here</p>
        <button @click="register">Register me!</button>
</template> 