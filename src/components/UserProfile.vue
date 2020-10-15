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

      <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot">New Twoot</label>
        <textarea
          name="newTwoot"
          id="newTwoot"
          cols="30"
          rows="10"
          v-model="newTwootContent"
        />

        <div class="user-profile__create-twoot-type">
          <label for="newTwootType">Type:</label>
          <select
            name="newTwootType"
            id="newTwootType"
            v-model="selectedTwootType"
          >
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>

        <button>Twoot!</button>
      </form>
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

export default {
  name: "UserProfile",
  components: { TwootsVue },
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
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
      newTwootContent: "",
      selectedTwootType: "instant",
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log(`my fav #${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType != "draft") {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },
  },
  mounted() {
    this.followUser();
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
  }
  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }

  .user-profile__create-twoot {
    display: flex;
    flex-direction: column;
    padding-top: 20px;
  }
}
</style>