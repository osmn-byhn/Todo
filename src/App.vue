<script setup>
  import Navbar from './components/Navbar.vue';
  import { ref, onMounted, computed, reactive } from "vue";
  const todoText = ref('')
  const deneme = ref([])
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
    console.log(todoArray.value.filter((todo) => todo.isCompleted === true).length);
    
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
    <progress
        :max="todoArray.length"
        :value="todoArray.filter((todo) => todo.isCompleted === true).length"
    ></progress>
    <div>Clear completed todos</div>
    <hr>
    <div class="form">
      <form>
        <input type="text" name="" id="todoText" v-model="todoText">
        <input type="submit" @click="addTodo()" value="Add" :disabled="todoText === ''" >
      </form>
    </div>
  </div>
  
  <div v-for="(item, index) in todoArray" >
    <p>{{ item.text }}</p>
  </div>
</template>

<style scoped lang="scss">
</style>
