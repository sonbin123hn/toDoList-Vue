<template>
    <AddTodos @add-todos="addTodos" />
    <TodosItem 
    v-for="todo in todos"
    :key="todo" 
    :todoProps="todo"
    @is-com="markCom"
    @delete-item="deleteItem"
    />
</template>

<script>
import {ref} from 'vue';
import TodosItem from './TodosItem.vue'
import AddTodos from './AddTodos.vue'
// import {v4 as uuidv4} from 'uuid'
import axios from 'axios'

export default {
    name: "Todos",
    components: {TodosItem, AddTodos},
    setup(){
        const todos = ref([])

        const getAllTodos = async () => {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
                todos.value = res.data
            } catch (error) {
                console.log(error)
            }
        }
        getAllTodos()

        const markCom = id  => {
            todos.value = todos.value.map(todo => {
                if(todo.id === id) todo.type = !todo.type;
                return todo;
                
            })
        }
        const deleteItem = async id => {
            //todos.value = todos.value.filter(todo => todo.id !== id)
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id) //front end
            } catch (error) {
                console.log(error)
            }
        }
        
        const addTodos = async newTodo => {
            //todos.value.push(newTodo);
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos',newTodo)
                todos.value.push(res.data)
            } catch (error) {
                console.log(error)
            }
        }

        return{
            todos,markCom,deleteItem,addTodos
        }
    }
}
</script>

<style>

</style>