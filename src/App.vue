<script setup>
  import {ref} from 'vue'

  let todos = ref(['A','B','C'])
  let newTodo = ref('')

  function addTodo () {
    todos.value.push({
      text: newTodo.value,
      complete: false
    })
    newTodo.value = ''

  }
  function deleteTodo (index) {
    todos.value.splice(index, 1)
  }

</script>

<template>
  <h1 >My To Do Application</h1>

  <ul>
    <li v-for="(todo, index) in todos">
      <input type="checkbox" v-model="todo.complete">
      {{ todo.text }}
      <button id="delete" @click="deleteTodo(index)">&#10060;</button>

    </li>
  </ul>

  <input v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo">Add Todo</button>
</template>

<style>
h1{
  text-align: center;
}




</style>
