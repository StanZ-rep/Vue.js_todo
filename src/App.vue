<template>
  <h1>ToDo list</h1>
  <form @submit.prevent="addNewTodo">
    <input v-model="newTodo" name="newTodo" />
    <button class="newTodo">Add New Todo</button>
  </form>
  <ul>
    <li v-for="(todo, index) in todos" v-bind:key="todo.id" class="todo">
      <h1 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h1>
      <button class="btn" @click="removeTodo(index)">Remove item</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
    };
  },
};
</script>

<style>
#app {
  background-color: rgb(252, 139, 1);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
  color: rgb(22, 3, 64);
  margin-top: 60px;
  padding: 15%;
  margin: 10%;
  max-width: 50%;
  min-height: 100%;
}

.todo {
  list-style-type: none;
  cursor: pointer;
  color: rgb(22, 3, 64);
  background-color: bisque;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
  max-width: 100%;
  box-sizing: border-box;
}

.done {
  text-decoration: line-through;
  color: bisque;
  border-style: inset;
  background-color: rgb(22, 3, 64);
}

.btn {
  background-color: rgb(22, 3, 64);
  color: bisque;
}
.newTodo {
  background-color: rgb(22, 3, 64);
  color: bisque;
}
</style>
