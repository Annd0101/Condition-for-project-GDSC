<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']" @dblclick="markItemCompleted">
    {{ todoProps.title }}
    <i class="fas fa-x" @click="deleteItem"></i>
  </p>
</template>

<script>
//import { ref } from 'vue'
export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.todoProps.id)
    }
    const deleteItem = () => {
      if (confirm(`Delete todo ?`))
      context.emit('delete-item', props.todoProps.id)
    }
    return {
      markItemCompleted,
      deleteItem
    }
  }
}
</script>

<style>
.todo-item {
  position: relative;
    background: #fffdfd;
    padding: 10px;
    width: 90%;
    margin: auto;
    padding: 12px 0;
    margin-top: 10px;
    margin-bottom: 8px;
    border-left: none;
    box-shadow: 1px 1px 2px 2px rgb(104, 104, 104);
    border-radius: 5px;
}



.todo-item:hover {
  background-color: rgb(229, 226, 226);
    
}
.is-completed {
   border-left: 10px solid greenyellow;;
}
p i {
position: absolute;
right: -600px;
top: 50%;
transform: translate(-50%, -50%);
font-size: 15px;
cursor: pointer;
transition: all 0.3 ease;
}
p:hover i{
  right: 5px;
}
</style>