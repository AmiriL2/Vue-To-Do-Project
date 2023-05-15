<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
  let newTodo = ref()
  let input = ref('')

  watch(todos, function(value) {
    window.localStorage.setItem('todos', JSON.stringify(value))
  }, {deep:true})

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
  <div class="container">
    <div class="todo-app">
  <h1 >To Do List</h1>
<div class="addtoDo">
  <input v-model="newTodo" @keydown.enter="addTodo">
  <button class="addbutton" @click="addTodo">Add Todo</button>
</div>
  <ul>
    <li v-for="(todo, index) in todos">
      <input type="checkbox" v-model="todo.complete">
      {{ todo.text }}
      <button id="delete" @click="deleteTodo(index)">&#10060;</button>
    </li>
  </ul>
    </div>
  </div>
</template>

<style>
h1{
  text-align: center;
  padding-bottom: 20px;
}

.container{
  width: 100%;
  min-height: 100vh;
  background: rgb(141, 140, 142);
}

.todo-app {
  width:100%;
  max-width: 540px;
  background-color: white;
  margin: 0px auto 20px;
  padding: 40px 30px 70px;
  border-radius: 10px;
  box-shadow: 5px 5px 5px 5px rgb(68, 68, 68);
}

.addbutton {
border: none;
outline: none;
padding: 8px 25px;
margin-left: 10px;
background: skyblue;
cursor: pointer;
border-radius: 24px;
box-shadow: 2px 2px 2px 2px rgb(106, 164, 186);
}
</style>
