<template>
  <form class="add-form"
  @submit="addItem"
  @input="check">
        <label class="label">
            <h2>Title</h2>
            <input type="text" v-model="title" />
            <button class="cancel" @click="closeform">Cancel</button>
            <button class="submit" @click="add-todo">Add</button>
        </label>
    </form>
</template>

<script >
import { ref } from 'vue'
// import { v4 as uuidv4 } from 'uuid'
export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')
    const addItem = event => {
      event.preventDefault()
      const newItem = {
        // id: uuidv4(),
        title: title.value,
        completed: false
      }
      if((newItem.title=='')){
        alert("Title is empty")
        return;
      }
      context.emit('add-todo', newItem)
     title.value=''
     
    }
   const closeform = event =>{
      event.preventDefault()
      context.emit('closeform')
    
    }
    return {
      title,
      addItem,
      closeform
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
}
input[type='text'] {
  flex: 10;
  padding: 5px;
}
input[type='submit'] {
  flex: 2;
}
.add-btn{
  border-radius: 5px;
}
.text-btn{
  border-radius: 5px;
}
input {
        width: 90%;
        margin: 15px 0;
        padding: 12px;
        border: 2px solid gray;
        background-color: rgb(247, 247, 247);
    }
.label {
  width: 100%;
}
.label input{
  border-radius: 5px;
}
 button {
        display: inline-block;
        width: 80px;
        height: fit-content;
        margin-left: 5px;
        padding: 5px;
        outline: none;
        border: none;
        border-radius: 5px;
        font-size: 15px;
    }
.cancel{
  margin-left: 300px;
}
    button:hover {
        cursor: pointer;
    }
    button.cancel {
        background-color: rgb(155, 148, 148);
    }
    button.cancel:hover {
        background-color: rgb(229, 226, 226);
    }
    button.submit {
        background-color: rgb(155, 148, 148);
    }
    button.submit:hover {
        background-color: rgb(229, 226, 226);
    }
</style>