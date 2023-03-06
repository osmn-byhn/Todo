<script setup>
  import Navbar from './components/Navbar.vue';
  import { reactive } from "vue";
  const todo = reactive({
    date: Date.now,
    text: '',
    isCompleted: false
  })
  function addTodo() {
    localStorage.setItem("mission", todo.text)
  }
  
  
</script>

<template>
  <Navbar />
  <div class="main">
    <progress max="1" value="0"></progress>
    <div>Clear completed todos</div>
    <hr>
    <div class="form">
      <form>
        <input type="text" name="" v-model="todo.text">
        <button @click="addTodo()">Add</button>
      </form>
    </div>
  </div>
  <div>{{ note }}</div>
</template>

<style scoped lang="scss">
  
</style>
