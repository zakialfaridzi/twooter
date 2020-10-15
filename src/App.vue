<template>
  <div id="app">
    <UserProfileVue />
  </div>
</template>

<script>
import UserProfileVue from "./components/UserProfile.vue";

export default {
  name: "App",
  components: { UserProfileVue },
};
</script>

<style>
#app {
  font-family: Inter, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #f3f5fa;
}
</style>
