<script setup >
  import {ref, computed } from 'vue'
  const todoText = ref(''),
  todoList = ref([]),
  pending = computed(() => {
    return todoList.value.filter(i => !i.checked)
  }),
  done = computed(() => {
    return todoList.value.filter(i => i.checked)
  })
  function clearToDo() {todoText.value = ''}
  function addToDo() {
    if (todoText.value && todoText.value !== '') {
      todoList.value.push({id: new Date().valueOf(), 
      text: todoText.value,
      checked: false})
      clearToDo()
    }
  }
</script>
<template>
  <div class="todo-container w3-white w3-card-4">
    <div class="w3-container w3-black w3-margin-0 w3-bottombar w3-border-blue">
      <h1>
        <i class="fa-solid fa-clipboard-list"> </i>
        To-Do-List
      </h1>
    </div>
    <div class="w3-container flex-container w3-light-gray w3-padding">
        <input class="w3-input w3-border-0" type="text" autofocus v-model="todoText" @keyup.enter="addToDo()" placeholder="Enter your to-do">
        <button class="w3-button w3-gray" @click="clearToDo()">
          <i class="fa-solid fa-times"></i>
        </button>
        <button class="w3-button w3-gray" @click="addToDo()">
          <i class="fa-solid fa-plus"></i>
        </button>
    </div>
    <div class="w3-padding w3-blue">
      Pending({{pending.length}})
    </div>
      <div class="w3-padding" v-for="todo in pending" :key="todo.id">
        <label>
          <input type="checkbox" v-model="todo.checked">
          <span class="w3-margin-left">
            {{todo.text}}
          </span>
        </label>
      </div>
      <div class="w3-padding" v-show="pending.length == 0">No tasks</div>
      <div class="w3-padding" v-for="todo in done" :key="todo.id">
        <label>
          <input type="checkbox" v-model="todo.checked">
          <span class="w3-margin-left">
            {{todo.text}}
          </span>
        </label>
      </div>
      <div class="w3-padding" v-show="done.length == 0">No tasks</div>

    </div>
</template>
<style scoped>
  
</style>
