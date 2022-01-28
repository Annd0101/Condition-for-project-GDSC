<template>
  <div class="container"> 
    <h1>Todo list</h1>
    <div class="content">
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    @item-completed="markComplete"
    @delete-item="deleteTodo"
  />
  <button class="showbutton">
  <i  class="fas fa-plus" 
      @click="isShowForm = true"
      v-if="!isShowForm"
  ></i></button>
 <AddTodo  v-if="isShowForm" 
          @add-todo="addTodo" 
          @closeform="isShowForm = false"
 />

  </div>
  </div>
</template>

<script>
import { ref } from 'vue'
// import { v4 as uuidv4 } from 'uuid'

import axios from 'axios'
import TodoItem from './TodoItem'
import AddTodo from './AddTodo'
export default {
  name: 'Todos',
  data: () => ({
    isShowForm: false,
  }),
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])
    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_start=0&_limit=5&_delay=3000'
        )
        // console.log(res.data)
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getAllTodos()
    const markComplete = id => {
      todos.value = todos.value.map(todo => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }
    const deleteTodo = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch (error) {
        console.log(error)
      }
    }
    const addTodo = async newTodo => {
      try {
        const res = await axios.post(
          'https://jsonplaceholder.typicode.com/todos',
          newTodo
        )
        todos.value.push(res.data)
      } catch (error) {
        console.log(error)
      }
    }
    
    return {
      todos,
      markComplete,
      deleteTodo,
      addTodo
    }
  }
  
}

</script>

<style>
.container {
  width: 40%;
  height: fit-content;
  margin: auto;
  margin-top: 10%;
  background-color: rgb(250, 248, 248);
  box-shadow:1px 1px 2px 2px rgb(78, 75, 75);
  border-radius: 15px 15px;
  text-align: center;
} 
button{
  width: 30px;
  height: 100%;
  border: none;
  outline: none;
  background:  #fff;
  color: #0f0f0f;
  cursor: pointer;
  border-radius: 3px;
  margin-left: 5px;
  font-size: 22px;
  cursor: pointer;
}

</style>