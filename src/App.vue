<template>
  <Navbar />
  <div class="app">
    <router-view />
  </div>
</template>

<style>
.app {
  text-align: center;
}
</style>

<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: { Navbar },
};
</script>
