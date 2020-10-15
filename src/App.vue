<template>
  <div id="app">
    <nav>
      <div class="navigation__logo">Twooter</div>
      <div class="navigation__user">
        {{ user.userName }}
      </div>
    </nav>
    <UserProfileVue />
  </div>
</template>

<script>
import UserProfileVue from "./components/UserProfile.vue";

export default {
  name: "App",
  components: { UserProfileVue },
  data() {
    return {
      user: {
        userName: "@zalfaridzii",
      },
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Inter, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #f3f5fa;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: deeppink;
    color: white;
    .navigation__logo {
      font-weight: bold;
      font-size: 24px;
    }
    .navigation__user {
      font-weight: bold;
    }
  }
}
</style>
