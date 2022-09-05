<script setup>
import { ref } from "vue";

const todoList = ref([]);
const todo = ref("");

const handleAddTaskToList = () => {
  if (!todo.value) return;

  todoList.value.push(todo.value);
  todo.value = "";

  return;
};

const handleRemoveTaskFromList = (todo) => {
  const newList = todoList.value.filter((task) => task !== todo);
  todoList.value = newList;
};
</script>

<template>
  <section class="p-6 bg-gray-100 min-h-screen">
    <div class="mx-auto max-w-sm shadow-xl rounded p-6 bg-white">
      <h1 class="text-2xl tracking-wide mb-2">Daily Agenda</h1>

      <p>
        Keep track of your daily tasks, and boost productivity and
        accountability!
      </p>

      <form @submit.prevent="handleAddTaskToList" class="mt-10">
        <div class="mb-4">
          <label class="block mb-2 font-semibold"
            >What will you be doing today?</label
          >

          <textarea
            v-model="todo"
            cols="30"
            rows="3"
            class="w-full block border border-2 bg-gray-50 rounded px-2"
            placeholder="I want to ..."
          ></textarea>
        </div>

        <button
          class="bg-blue-600 py-2 px-6 rounded text-white font-bold text-center"
        >
          Add task
        </button>
      </form>
    </div>

    <div class="mx-auto max-w-sm shadow-xl rounded p-6 bg-white mt-5">
      <div v-if="todoList.length">
        <h1 class="text-lg font-semibold tracking-wide mb-2">
          Your today's tasks
        </h1>

        <p>Hi. Here's what you planned to do today:</p>

        <ul class="mt-8">
          <li
            v-for="todo in todoList"
            :key="todo"
            class="border shadow-md p-3 rounded bg-gray-50 mb-4 text-sm tracking-wide flex justify-between"
          >
            <span>{{ todo }}</span>

            <span
              @click="handleRemoveTaskFromList(todo)"
              class="text-xs text-red-600 font-bold ml-4 cursor-pointer"
              >Remove</span
            >
          </li>
        </ul>
      </div>

      <div v-else>
        <p class="font-bold tracking-wide">Oops...</p>
        <p>
          You don't have any task set for today! Add a task now to see them
          here.
        </p>
      </div>
    </div>
  </section>
</template>
