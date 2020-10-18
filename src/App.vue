<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">twooter</div>
      </router-link>
      <div class="navigation__user" v-if="user">@{{ user.username }}</div>
    </nav>
    <router-view />
    <section class="curved"></section>
  </div>
</template>

<script>
import { computed } from "vue";
import { useStore } from "vuex";
export default {
  name: "App",
  setup() {
    const store = useStore();
    const user = computed(() => {
      return store.state.User.user;
    });

    return { user };
  },
};
</script>

<style lang="scss">
#app {
  font-family: DM Sans, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: whitesmoke;
  min-height: 100vh;
  background-color: #16202a;
  position: relative;
  background: #2c3e50;
  height: 50vh;
  margin: auto;
  padding: auto;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: #1da1f2;
    color: black;

    .navigation__logo {
      font-weight: bold;
      font-size: 24px;
      z-index: 1;
      position: relative;
    }

    .navigation__user {
      font-weight: bold;
    }
  }

  #app::after {
    content: "";
    border-top-left-radius: 50% 100%;
    border-top-right-radius: 50% 100%;
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    background: #f5f5f5;
    height: 32%;
  }
}
</style>
