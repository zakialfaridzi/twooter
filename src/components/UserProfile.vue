<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.userName }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Chadmin</div>
      <div
        class="user-profile__admin-badge"
        v-else
        style="background: #4fba8a; color: #334b5d"
      >
        Virgin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers</strong>: {{ followers }}
      </div>
      <TwootsPanelVue @add-twoot="addTwoot" />
    </div>

    <div class="user-profile__twoots-wrapper">
      <TwootsVue
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.userName"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TwootsVue from "./Twoots.vue";
import TwootsPanelVue from "./TwootsPanel.vue";

export default {
  name: "UserProfile",
  components: { TwootsVue, TwootsPanelVue },
  data() {
    return {
      followers: 0,
      following: 1,
      isLoading: false,
      user: {
        id: 1,
        userName: "zalfaridzii",
        firstName: "Zaki",
        lastName: "Al Faridzi",
        email: "zalf@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "twooter🔥🔥" },
          { id: 2, content: "#FFXVI" },
          { id: 3, content: "#WOODWARDOUT" },
          { id: 4, content: "#MUNTOT1-6" },
        ],
      },
    };
  },
  methods: {
    addTwoot(twoot) {
      this.user.twoots.unshift({
        id: this.user.twoots.length + 1,
        content: twoot,
      });
    },
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.userName} have a new follower`);
      }
    },
  },
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
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
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