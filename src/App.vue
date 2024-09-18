<script setup>
import { inject } from 'vue'
const GStore = inject('GStore')
</script>

<template>
  <div id="layout">
  <header>
    <div id="flashMessage" v-if="GStore.flashMessage">
      {{ GStore.flashMessage }}
    </div>
    <div class="wrapper">
      <nav>
        <RouterLink :to="{ name: 'event-list'}">Events</RouterLink> |
        <RouterLink :to="{ name: 'about'}">About</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView />
  </div>
</template>

<style>
@keyframes yellowfade {
  from {
    background: yellow;
  }
  to {
    background: transparent;
  }
}

#flashMessage {
  animation-name: yellowfade;
  animation-duration: 3s;
}

#layout {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1f2d3b;
}
nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a.router-link-exact-active {
  color: #42b983;
}

h2 {
  font-size: 20px;
}
</style>
