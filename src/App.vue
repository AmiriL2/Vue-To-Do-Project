<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
  let newTodo = ref()
  let input = ref('')
  let filter = ref('all')

  watch(todos, function(value) {
    window.localStorage.setItem('todos', JSON.stringify(value))
  }, {deep:true})

  function activeFilter(todo){
    return todo.complete == false
  }

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

  function clearTodo () {
    todos.value = []
  }

  function todoFilter (todo) {
    if (filter.value == 'active') {
      return todo.complete == false;
    } else if (filter.value == 'completed'){
      return todo.complete == true;
    }
    return true;
  }

</script>

<template>
  <div class="container2">
    <div class="todo-app">
  <h1 >To Do List</h1>
  <p v-if="todos.length > 0">
  <div class="radios">
  <input name="filter" type="radio" value="all" v-model="filter">
    <label>All</label>

    <input name="filter" type="radio" value="active" v-model="filter">
    <label>Active</label>

    <input name="filter" type="radio" value="completed" v-model="filter">
    <label>Completed</label>
  </div>
</p>
<div class="addtoDo">
  <input class="input1" v-model="newTodo" @keydown.enter="addTodo">
  <button class="addbutton" @click="addTodo">Add Todo</button>
  <button class="clearbutton" @click="clearTodo">Clear</button>
</div>
    <p v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}" >
      <label class="container">
  <input type="checkbox" v-model="todo.complete" checked="checked">
  <span class="checkmark"></span>
</label>
      {{ todo.text }}
      <button id="delete" @click="deleteTodo(index)">&#10060;</button>
  </p>
  <div class="amount">
  <p v-if="todos.length > 0"></p>
  <p>{{todos.filter(activeFilter).length}} Items</p>
</div>
    </div>
  </div>
</template>

<style>
h1 {
  text-align: center;
  padding-bottom: 20px;
}

.container2 {
  margin-top: 10px;
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
background: rgb(193, 193, 193);
cursor: pointer;
border-radius: 5px;
box-shadow: 2px 2px 2px 2px rgb(62, 62, 62);
min-width: 20px;
}

.addbutton:hover {
  background-color: rgb(52, 52, 52);
  transition: ease-in 250ms;
  color: white;
}

.input1 {
    width: 60%;
    border: none;
    border-bottom: 1px solid #16161a;
    outline: none;
    padding-top: px;
    padding-bottom: 5px;
    padding-left: 5px;
    text-align: center;
  font-size: 20px;
  font-family: 'Braah One', sans-serif;

}

/* Customize the label (the container) */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #2196F3;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.completed {
  text-decoration: line-through;
  color: #c2c2c2;
}

#delete {
  border: none;
  outline: none;
  height: 25px;
  width: 25px;
  background-color: #eee;
  float: right;
}

p {
  text-align: center;
  font-size: 20px;
  font-family: 'Braah One', sans-serif;
}

#delete:hover {
  background-color: #ccc;
  cursor: pointer;
}

.radios {
display: flex;
justify-content: center;
padding-bottom: 40px;
flex-direction: column;
}

input {
  cursor: pointer;
}

label {
  font-size: 15px;
  font-family: 'Braah One', sans-serif;
}

.amount {
  padding-top: 10px;
}

.clearbutton {
border: none;
outline: none;
padding: 8px 25px;
margin-left: 10px;
background: rgb(247, 61, 61);
cursor: pointer;
border-radius: 5px;
box-shadow: 2px 2px 2px 2px rgb(62, 62, 62);
}

.clearbutton:hover {
  background-color: rgb(185, 5, 5);
  transition: ease-in 250ms;
}
</style>