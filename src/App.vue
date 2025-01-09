<template>
  <div class="todolist">
    <AddTodo @add-todo="handleAddTodo" />
    <TodoList :todos="todos" @delete-todo="handleDelete" @complete-todo="handleComplete" />
  </div>
</template>

<script setup>
import AddTodo from './components/AddTodo.vue'
import TodoList from './components/TodoList.vue'
import { ref, onMounted, watch } from 'vue'

const todos = ref([])

const handleAddTodo = (todo) => {
  if (todo.content.length > 0) {
    todos.value.push(todo)
  } else {
    alert('請填入待辦事項！！')
  }
}

const handleDelete = (todoId) => {
  todos.value = todos.value.filter((todo) => todo.id !== todoId)
}

const handleComplete = (todoId) => {
  todos.value = todos.value.map((todo) =>
    todo.id === todoId ? { ...todo, complete: !todo.complete } : todo,
  )
}

onMounted(() => {
  const saveTodos = JSON.parse(localStorage.getItem('todos')) || []
  todos.value = saveTodos
})
watch(
  todos,
  (newTodos) => {
    localStorage.setItem('todos', JSON.stringify(newTodos))
  },
  { deep: true },
)
</script>

<style scoped>
* {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}
</style>
