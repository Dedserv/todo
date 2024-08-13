<template>
  <TransitionGroup class="task" name="list" tag="ul">
    <li
      class="task__element relative border-solid border border-light-blue-500 rounded-xl drop-shadow-md p-4 mb-2"
      :class="task.status === 'isDeleted' ? 'task__deleted' : ''"
      v-for="task in tasks"
      :key="task.id"
    >
      <p class="align-middle inline-block">{{ task.text }}</p>
      <button
        class="text-red-500 hover:text-red-400 ease-in duration-300"
        @click="onClickDeleteButton(task)"
      >
        <TrashIcon
          class="absolute top-1/2 -translate-y-1/2 right-4 size-5 text-inherit"
        />
      </button>
    </li>
  </TransitionGroup>
</template>
<script setup>
import { TrashIcon } from "@heroicons/vue/24/solid";

defineProps({
  tasks: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["deleteTaskHandler"]);

const onClickDeleteButton = (task) => {
  task.status = "isDeleted";
  emit("deleteTaskHandler", task.id);
};
</script>
<style>
.task__element {
  box-sizing: border-box;
  overflow: hidden;
  height: 60px;
}

.list-enter-active,
.list-leave-active {
  opacity: 1;
  transition: all 1s ease;
  height: calc-size(auto);
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  padding: 0;
  margin: 0;
  height: 0;
}
</style>
