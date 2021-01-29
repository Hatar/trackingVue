<template>
  <div class="container">
    <Navbar />
  </div>
  <router-view />
</template>
<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: {
    Navbar
  }
};
</script>
<style>
body {
  font-family: "Nunito Sans", sans-serif;
}
</style>
