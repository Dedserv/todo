<template>
  <div class="absolute top-0 left-1/2 -translate-x-1/2 w-2/4">
    <h1 class="text-4xl mt-10">Список задач</h1>
    <ul class="mt-5">
      <li
        class="relative animate-pulse border-solid border border-light-blue-500 bg-slate-100 rounded-xl p-4 mb-2"
        v-for="(task, index) in 5"
        :key="`${index}_skeleton`"
      >
        <p
          class="align-middle inline-block rounded-xl bg-slate-200 text-transparent"
        >
          The name of the task and its description.
        </p>
      </li>
    </ul>
  </div>
</template>
<style scoped></style>
