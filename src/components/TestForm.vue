<template>
  <v-container class="fill-height">
    <v-sheet class="mx-auto" width="300">
      <v-form @submit.prevent="handleSubmit">
        <v-text-field
          v-model="form.email"
          placeholder="johndoe@gmail.com"
          label="Email"
        ></v-text-field>

        <div v-if="v$.email.$error" class="text-subtitile-1 text-red pt-0">
          {{ v$.email.$errors[0].$message }}
        </div>

        <v-text-field v-model="form.password" label="Password"></v-text-field>
        <div v-if="v$.password.$error" class="text-subtitile-1 text-red pt-0">
          {{ v$.password.$errors[0].$message }}
        </div>
        <v-btn class="mt-2" type="submit" block>Submit</v-btn>
      </v-form>
    </v-sheet>
  </v-container>
</template>

<script setup lang="ts">
import { reactive, computed } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { minLength, required, email, sameAs } from "@vuelidate/validators";
import { useRouter, useRoute } from "vue-router";
import { router } from "@/router";
const form = reactive({
  email: "",
  password: "",
});
const rules = computed(() => {
  return {
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6),
    },
  };
});

const v$ = useVuelidate(rules, form);
async function handleSubmit() {
  const result = await v$.value.$validate();
  if (!result) {
  } else {
    router.push("/game");
  }
}
</script>
