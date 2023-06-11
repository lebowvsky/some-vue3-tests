<template>
  <h1>ABOOOOOOUUUUT !</h1>
  <form class="form" @submit.prevent="submit">
    <InputTextParticle
      label="Identifiant"
      type="email"
      name="email"
      v-model:modelValue="formData.email"
      :errorMessage="v$.email.$errors.length && v$.email.$errors[0].$message"
    />
    <InputTextParticle
      label="Mot de passe"
      type="password"
      name="password"
      v-model:modelValue="formData.password"
    />
    <button type="submit">Soumettre</button>
  </form>
</template>
<script setup lang="ts">
import InputTextParticle from "../particles/InputTextParticle.vue";
import { useVuelidate } from "@vuelidate/core";
import { required, email, minLength, helpers } from "@vuelidate/validators";
import { reactive, computed } from "vue";

const formData = reactive<{
  email: string;
  password: string;
}>({ email: "", password: "" });

const rules = computed(() => {
  return {
    email: { required, email },
    password: {
      required: helpers.withMessage("veuillez remplir ce champ", required),
      minLength: minLength(8),
    },
  };
});

const v$ = useVuelidate(rules, formData);

const submit = async () => {
  const result = await v$.value.$validate();
  console.log(result);
  if (result) {
    console.log("Hop !");
  } else {
    console.log("Pas bon !!! :(");
  }
};
</script>
