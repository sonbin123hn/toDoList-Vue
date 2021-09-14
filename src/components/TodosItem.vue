<template>
    <p :class="['todosItem',todoProps.type ? 'is-com' : '']">
        <input type="checkbox" :checked="todoProps.type" @change="markItemCom"> 
        {{ todoProps.title }}
        <button class="del-btn" @click="deleteItem">Delete</button>
    </p>
</template>

<script>
export default {
    name: "TodosItem",
    props: ['todoProps'],
    setup(props, context){
        const markItemCom = () => {
            context.emit('is-com',props.todoProps.id)
        }
        const deleteItem = () => {
            context.emit('delete-item',props.todoProps.id)
        }
        return {
            markItemCom,deleteItem
        }
       
    }
}
</script>

<style>
.del-btn{
    background: #ff0000;
    color: #fff;
    border: none;
    cursor: pointer;
    float: right;
}
.is-com {
    text-decoration: line-through;
}
.todosItem{
    background: #f4f4f4;
    padding: 10px;
    margin: 0;
    border-bottom: 1px #ccc dotted;
}

</style>