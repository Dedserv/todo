<template>
  <form class="flex items-center gap-2">
    <input
      placeholder="Добавьте задачу"
      class="rounded-md border-2 p-2 text-gray-900"
      :class="{ 'border-blue-400 outline-none': isFocus }"
      type="text"
      v-model="text"
      @focus="isFocus = true"
      @focusout="isFocus = false"
    />
    <button @click.prevent="$emit('onSubmitButtonHandle')">
      <PlusCircleIcon class="size-10 text-blue-500" />
    </button>
  </form>
</template>
<script setup>
import { ref } from "vue";
import { PlusCircleIcon } from "@heroicons/vue/24/solid";
const text = defineModel();
defineEmits(["onSubmitButtonHandle"]);
const isFocus = ref(false);
</script>
