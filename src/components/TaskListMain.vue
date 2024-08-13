<template>
  <div class="m-auto w-2/4">
    <h1 class="text-4xl mt-10" v-html="taskTitle" />
    <div class="mt-5">
      <TaskList
        v-if="tasksList?.data?.length"
        :tasks="tasksList.data"
        @deleteTaskHandler="deleteTaskHandler"
      />
    </div>
    <TaskCreate v-model="taskText" @onSubmitButtonHandle="createTaskHandler" />
  </div>
</template>

<script setup>
import { reactive, ref, computed, inject } from "vue";
import TaskList from "../components/TaskList.vue";
import TaskCreate from "../components/TaskCreate.vue";
const axios = inject("axios");

const tasksList = reactive({ data: [] });
const taskText = ref("");

const fetchData = async () => {
  const res = await fetch(
    "https://667d3095297972455f63f0d2.mockapi.io/api/tasks"
  );
  tasksList.data = await res.json();
};

const { data } = await axios.get(
  "https://667d3095297972455f63f0d2.mockapi.io/api/tasks"
);
console.log(data);
await fetchData();

const maxId = computed(() => {
  const maxidTask = tasksList.data.reduce((maxId, task) => {
    return maxId > task.id ? maxId : task.id;
  }, 0);
  return Number(maxidTask) + 1;
});

const taskTitle = computed(() =>
  tasksList.data.length ? "Список задач" : "Список задач пуст"
);

const createTaskHandler = () => {
  const newTask = {
    id: maxId.value || 1,
    text: taskText.value,
  };
  fetch("https://667d3095297972455f63f0d2.mockapi.io/api/tasks", {
    method: "post",
    headers: { "content-type": "application/json" },
    body: JSON.stringify(newTask),
  })
    .then((response) => {
      if (response.ok) {
        taskText.value = "";
        tasksList.data = [...tasksList.data, newTask];
      }
    })
    .catch((e) => console.log(e));
};

const deleteTaskHandler = async (id) => {
  await fetch(`https://667d3095297972455f63f0d2.mockapi.io/api/tasks/${id}`, {
    method: "delete",
  })
    .then((response) => {
      if (response.ok) {
        taskText.value = "";
        tasksList.data = tasksList.data.filter((task) => {
          return id != task.id;
        });
      }
    })
    .catch((e) => console.log(e));
};
</script>
