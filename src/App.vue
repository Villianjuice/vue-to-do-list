<template>
  <Navbar />
  <router-view />
</template>

<script setup>
import Navbar from "./components/Navbar.vue"

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial,  sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: gray;
}
</style>