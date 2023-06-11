<template>
  <div class="form-item">
    <label class="form-item_label" :for="name">{{ label }}</label>
    <input
      class="form-item_input"
      :type="type"
      :name="name"
      :id="name"
      @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
    />
    <p v-if="errorMessage">{{ errorMessage }}</p>
  </div>
</template>
<script lang="ts" setup>
import { watch } from "vue";

const props = withDefaults(
  defineProps<{
    label: string;
    type?: "text" | "email" | "password";
    name: string;
    modelValue: string | unknown;
    errorMessage?: string;
  }>(),
  {
    type: "text",
  }
);

watch(
  () => props.errorMessage,
  () => {
    console.log(props.errorMessage);
  }
);
</script>
<style scoped>
.form-item {
  display: flex;
  flex-direction: column;
  width: 300px;
  gap: 5px;
}
.form-item_label {
  color: rgb(184, 184, 235);
}
.form-item_input {
  background-color: rgb(241, 247, 250);
  border: solid 1px rgb(155, 158, 165);
  border-radius: 4px;
  height: 45px;
}
</style>
