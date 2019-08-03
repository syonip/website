<template>
  <q-page class="flex flex-center">
    <div class="row full-width justify-center">Current Username: {{name}}</div>
    <div class="row full-width justify-center">
      <q-btn @click="prompt = true">Open Dialog</q-btn>
    </div>
    <q-prompt-validation-dialog
      ref="myDialog"
      :input-value="name"
      :show-dialog="prompt"
      :rules="[validateName]"
      header-text="Choose a nickname"
      @hide="hide"
      @ok="usernameChanged"
      persistent
    />
  </q-page>
</template>

<style>
</style>

<script>
import QPromptValidationDialog from "quasar-prompt-validation-dialog";

export default {
  name: "PageIndex",
  data() {
    return {
      prompt: false,
      name: "my initial name"
    };
  },
  components: {
    QPromptValidationDialog
  },
  methods: {
    validateName(name) {
      return new Promise(async (resolve, reject) => {
        setTimeout(() => { // For demonstrating async validations
          if (name.length < 3)
            return resolve("Name must have at least 3 characters");
          if (name.length > 20)
            return resolve("Name length can't exceed 10 characters");
          if (!name) return resolve("You must enter your name!");

          return resolve(true);
        }, 1000);
      });
    },
    async usernameChanged(name) {
      // Do what you need with the value here
      this.name = name;
    },
    hide() {
      this.prompt = false;
    }
  }
};
</script>
