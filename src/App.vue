<script setup>
import { ref, onMounted, computed, watch } from "vue";
const todo = ref({});
const name = ref("");

const input_content = ref("");
const input_category = ref(null);

const addTodo = () => {
  if (input_content.value.trim === "" || input_content.value === null) {
    return;
  }
  console.log("addTodo");
};

//ascending
const todo_asc = computed(() =>
  todos.value.sort((a, b) => {
    return b.createdAt - a.createdAt;
  })
);

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
});
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h1 class="title">
        what's up <input type="text" placeholder="Name here" v-model="name" />
      </h1>
    </section>

    <section class="create-todo">
      <h3>CREATE A TODO</h3>
      <form @submit.prevent="addTodo">
        <h4>What's on your todo list</h4>
        <input
          type="text"
          placeholder="e.g make a video"
          v-model="input_content"
        />
        <h4>Pick category</h4>
        <div class="options">
          <label>
            <input
              type="radio"
              name="category"
              value="business"
              v-model="input_category"
            />
            <span class="bubble business"></span>
            <div>business</div>
          </label>
          <label>
            <input
              type="radio"
              name="category"
              value="personnal"
              v-model="input_category"
            />
            <span class="bubble personnal"></span>
            <div>personnal</div>
          </label>
        </div>
        <input type="submit" value="Add todo" />
      </form>
    </section>
  </main>
</template>
