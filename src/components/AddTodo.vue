<template>
  <div>
    <form class="form" @submit.prevent="onSubmit">
      <h1>每日待辦事項</h1>
      <input type="text" class="form-input" v-model="text" />
      <button type="submit" class="form-button">加入</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { defineEmits } from 'vue'

const text = ref('')

const emit = defineEmits(['addTodo'])

const onSubmit = () => {
  if (text.value.trim()) {
    const todo = {
      id: crypto.randomUUID(),
      content: text.value,
      complete: false,
    }
    emit('addTodo', todo)
    text.value = ''
  }
}
</script>

<style>
div {
  display: flex;
  justify-content: center;
}
.form {
  display: flex;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  margin: 30px;
}
.form-input {
  height: 40px;
  border: 0.8px solid black;
  font-size: 1.1em;
  margin-top: 10px;
}
.form-button {
  height: 30px;
  margin-top: 10px;
  font-size: 1em;
}
button{
  cursor: pointer;
}
button:hover{
  font-weight: bold;
}
h1{
  letter-spacing: 0.5em;
}
</style>
