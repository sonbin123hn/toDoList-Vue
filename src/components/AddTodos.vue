<template>
  <form @submit="addItem">
      <input type="text" placeholder="Enter ..." 
      v-model="title" >
      <input type="submit" value="thêm" class="add-btn">
  </form>
</template>

<script>
import { ref } from '@vue/reactivity'
//import {v4 as uuidv4} from 'uuid'


export default {
    name: "AddTodos",
    setup(props,context) {
        const title = ref('');
        const addItem = event =>{
            event.preventDefault();
            const newItem = {
                //id: uuidv4(),
                title: title.value,
                completed: false,
            }
            context.emit("add-todos", newItem);

        }
        return {
            title,addItem,
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}
input[type="text"]{
    flex: 10;
    padding: 5px;
}
input[type="submit"]{
    flex: 2;
}

</style>