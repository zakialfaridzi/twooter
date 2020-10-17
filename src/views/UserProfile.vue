<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ state.user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Chadmin
        </div>
        <div
          class="user-profile__admin-badge"
          v-else
          style="background: #4fba8a; color: #334b5d"
        >
          Peasant
        </div>
        <div class="user-profile__follower-count">
          <strong>Followers</strong>: {{ state.followers }}
        </div>
      </div>
      <TwootsPanelVue @add-twoot="addTwoot" />
    </div>

    <div class="user-profile__twoots-wrapper">
      <TwootsVue
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import TwootsVue from "../components/Twoots.vue";
import TwootsPanelVue from "../components/TwootsPanel.vue";
import { useRoute } from "vue-router";
import { users } from "../assets/users";

export default {
  name: "UserProfile",
  components: { TwootsVue, TwootsPanelVue },
  setup() {
    const route = useRoute();

    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      following: 1,
      isLoading: false,
      user: users[userId.value - 1] || users[0],
    });

    function addTwoot(twoot) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: twoot,
      });
    }

    return {
      state,
      addTwoot,
      userId,
    };
  },

  // watch: {
  //   followers(newFollowerCount, oldFollowerCount) {
  //     if (oldFollowerCount < newFollowerCount) {
  //       console.log(`${this.user.userName} have a new follower`);
  //     }
  //   },
  // },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: #16202a;
    border-radius: 5px;
    border: 3px solid #1da1f2;
    margin-bottom: auto;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin: auto;
      padding: 0 10px;
      font-weight: bold;
    }

    .user-profile__create-twoot {
      display: flex;
      flex-direction: column;
      padding-top: 20px;

      &.--exceeded {
        color: red;
        border-color: red;
        button {
          background-color: red;
          color: white;
        }
      }
    }
  }

  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>