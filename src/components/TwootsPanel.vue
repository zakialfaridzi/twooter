<template>
  <form
    class="user-profile__create-twoot"
    @submit.prevent="createNewTwoot"
    :class="{ '--exceeded': newTwootCharCount > 180 }"
  >
    <label for="newTwoot">New Twoot ({{ newTwootCharCount }}/180)</label>
    <textarea
      name="newTwoot"
      id="newTwoot"
      cols="30"
      rows="10"
      v-model="newTwootContent"
    />

    <div class="user-profile__create-twoot-type">
      <label for="newTwootType">Type:</label>
      <select name="newTwootType" id="newTwootType" v-model="selectedTwootType">
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
</template>

<script>
export default {
  name: "TwootsPanel",
  data() {
    return {
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
      newTwootContent: "",
      selectedTwootType: "instant",
    };
  },
  computed: {
    newTwootCharCount() {
      return this.newTwootContent.length;
    },
  },
  methods: {
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType != "draft") {
        this.$emit("add-twoot", this.newTwootContent);
        this.newTwootContent = "";
        console.log("tw ad");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }
  .create-twoot-panel__submit {
    display: flex;
    justify-content: space-between;
    .create-twoot-type {
      padding: 10px 0;
    }
    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
    .create-twoot-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>
