<script setup>
  import Navbar from './components/Navbar.vue';
  import { ref, onMounted, computed } from "vue";
  /*
  const text = ref('')
  const todos = []
  function addTodo() {
    todos.push({
      id: Date.now(),
      text: text.value,
      isCompleted: false
    })
    text.value = ''
    localStorage.setItem('todos', JSON.stringify(todos))
  }
  onMounted(() => {
    
    todos.push(localStorage.getItem('todos'))
    console.log(todos)
    console.log('App mounted!')
    if (localStorage.getItem('todos')) {
      todos.value = JSON.parse(localStorage.getItem('todos'))
    }
    /*
    for (let index = 0; index < todos.length; index++) {
      todoItem.value = todos.value[index];
    }
  })*/

  const todoText = ref('')

  const todo = {
    id: String,
    text: String,
    isCompleted: Boolean
  }
  const todoArray = ref([])

  const completdTodos = computed(() => {
    todoArray.value.filter((todo) => todo.isCompleted === true)
  })
  
  const unCompletdTodos = computed(() => {
    todoArray.value.filter((todo) => todo.isCompleted === false)
  })

  const todoKey = "_vue_todos"

  function updateLocalStorage() {
    localStorage.setItem(todoKey, JSON.stringify(todoArray.value))
  }

  onMounted(() => {
    if (localStorage.getItem(todoKey) === null) {
      todoArray.value = []
    } else {
      try {
        todoArray.value = JSON.parse(localStorage.getItem(todoKey))
      } catch (e) {
        todoArray.value = []
      }
    }
    updateLocalStorage()
  })

  

  function addTodo() {
    todoArray.value = [
      ...todoArray.value,
      {
        id: Date.now(),
        isCompleted: false,
        text: todoText.value
      }
    ]
    updateLocalStorage()
    todoText.value = ''
  }


</script>

<template>
  <Navbar />
  <div class="main">
    <progress max="1" value="0"></progress>
    <div>Clear completed todos</div>
    <hr>
    <div class="form">
      <div>
        <input type="text" name="" id="todoText" v-model="todoText">
        <input type="submit" @click="addTodo()" value="Add" :disabled="todoText === ''">
      </div>
    </div>
  </div>
  
  <div v-for="(item, index) in todoArray" >
    <p>{{ item.text }}</p>
  </div>
</template>

<style scoped lang="scss">
</style>
