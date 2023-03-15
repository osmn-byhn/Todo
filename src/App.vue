<script setup>
  import Navbar from './components/Navbar.vue';
  import { ref, onMounted, computed, reactive } from "vue";
  const todoText = ref('')
  const todo = {
    id: String,
    text: String,
    isCompleted: Boolean
  }
  const todoKey = "_vue_todos"
  const todoArray = ref([])

  const completedTodos = computed(() => {
    deneme.value = todoArray.value.filter((todo) => todo.isCompleted === true).length
  })
  
  const unCompletedTodos = computed(() => {
    todoArray.value.filter((todo) => todo.isCompleted === false)
  })

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

  function toggleTodo(id) {
    todoArray.value.forEach((todo) => {
      if(todo.id === id ) todo.isCompleted = !todo.isCompleted
    })
    updateLocalStorage()
  }
  
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

  function select() {
    
    if (todoBoolean === true) {
      console.log("true");
      todoBoolean.value = false
    }
    else {
      console.log("false");
      todoBoolean.value = true
    }
  }
  
  function clearCompletedTodos() {
    todoArray.value = todoArray.value.filter((todo) => todo.isCompleted === false)
    updateLocalStorage()
  }
</script>

<template>
  <Navbar />
  <div class="main">
    <div class="buttons">
      <ul>
        <li >
          <span @click="clearCompletedTodos()" class="delete">Clear completed todos</span>
        </li>
        <li>
          <span class="text">{{ todoArray.filter((todo) => todo.isCompleted === true).length }} out of {{ todoArray.length }} completed</span>
        </li>
      </ul>
    </div>
    <progress
        :max="todoArray.length"
        :value="todoArray.filter((todo) => todo.isCompleted === true).length"
        class="progressBar"
    ></progress>
    <div class="form">
      <form>
        <input type="text" name="" class="todo-text" v-model="todoText">
        <input type="submit" @click="addTodo()" value="Add" :disabled="todoText === ''" class="button">
      </form>
    </div>
  </div>
  <div class="todo-list" v-for="(item, index) in todoArray" >
    <ul>
      <li>
        <input 
          type="checkbox" 
          name="isCompleted" 
          :id="item.id" 
          :checked="item.isCompleted"
          @change="toggleTodo(item.id)"
        />
      </li>
      <li>
        <label :for="item.id" :class="item.isCompleted ? 'completed' : 'incomplete'">{{ item.text }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
  @import '../public/App.scss'
</style>
