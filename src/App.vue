<template>
  <Transition name="fade">
    <Suspense>
      <TaskListMain />

      <template #fallback>
        <Loader />
      </template>
    </Suspense>
  </Transition>
</template>

<script setup>
import Loader from "./components/UI/Loader.vue";
import { defineAsyncComponent } from "vue";

const TaskListMain = defineAsyncComponent({
  loader: () => import("./components/TaskListMain.vue"),
});
</script>
<style>
.fade-enter-active,
.fade-leave-active {
  opacity: 1;
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
