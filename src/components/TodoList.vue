<template>
  <div class="todos-item" v-if="todos.length > 0">
    <ul v-for="todo in todos" :key="todo.id">
      <button id="but-complete" @click="completeTodo(todo.id)">V</button>
      <button id="but-delete" @click="deleteTodo(todo.id)">X</button>
      <li :class="{ iscomplete: todo.complete }">{{ todo.content }}</li>
    </ul>
  </div>
  <p v-else>No todo!</p>
</template>

<script setup>
import { defineProps } from 'vue'

const emit = defineEmits(['deleteTodo', 'completeTodo'])

const deleteTodo = (todoId) => {
  emit('deleteTodo', todoId)
}

const completeTodo = (todoId) => {
  emit('completeTodo', todoId)
}

defineProps({
  todos: {
    type: Array,
  },
})
</script>

<style>
ul {
  list-style: none;
  display: flex;
  gap: 10px;
}
li {
  margin-left: 10px;
  font-size: 20px;
}
.iscomplete {
  text-decoration: line-through;
  text-decoration-thickness: 2px;
}
p {
  margin: auto;
  padding: 20px;
  font-size: 25px;
}
</style>
