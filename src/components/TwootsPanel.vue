<template>
  <form
    class="create-twoot-panel"
    @submit.prevent="createNewTwoot"
    :class="{ '--exceeded': newTwootCharCount > 180 }"
  >
    <label for="newTwoot">New Twoot ({{ newTwootCharCount }}/180)</label>
    <textarea
      name="newTwoot"
      id="newTwoot"
      cols="30"
      rows="10"
      v-model="state.newTwootContent"
    />

    <div class="create-twoot-panel__submit">
      <div class="create-twoot-type">
        <label for="newTwootType">Type:</label>
        <select
          name="newTwootType"
          id="newTwootType"
          v-model="state.selectedTwootType"
        >
          <option
            :value="option.value"
            v-for="(option, index) in state.twootTypes"
            :key="index"
          >
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>Twoot!</button>
    </div>
  </form>
</template>

<script>
import { computed, reactive } from "vue";
export default {
  name: "TwootsPanel",
  setup(props, context) {
    const state = reactive({
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
      newTwootContent: "",
      selectedTwootType: "instant",
    });

    const newTwootCharCount = computed(() => {
      return state.newTwootContent.length;
    });

    function createNewTwoot() {
      if (state.newTwootContent && state.selectedTwootType != "draft") {
        context.emit("add-twoot", state.newTwootContent);
        state.newTwootContent = "";
        console.log("tw ad");
      }
    }

    return {
      state,
      newTwootCharCount,
      createNewTwoot,
    };
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
    background-color: #16202a;
    border: 3px solid #1da1f2;
    border-radius: 5px;
    color: white;
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
      background-color: #1da1f2;
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
