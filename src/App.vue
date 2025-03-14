

<template>
  <div class="row">
    <div class="col-md">
      <AddTodo @todoEmitted="handleTodo"/>
    </div>
  </div>
   
  <div class="row">
    <div class="col-md">
      <TodoList :todos="todos" @todoDeleted="deleteOneTodo"/>
    </div>
  </div>
</template>
<script setup>
import TodoList from './components/TodoList.vue'
import AddTodo from './components/AddTodo.vue'
import {ref,onMounted} from 'vue'
import { useToast} from "vue-toastification";

const toast = useToast();

const getId= ()=>{
 return  Math.floor(Math.random() * 100000)
} 
const todos = ref([])

onMounted(()=>{
const saveTodos= JSON.parse(localStorage.getItem('todos'))
if(saveTodos)
todos.value = saveTodos
})

const handleTodo= (todoData)=>{
todos.value.push({
taskName: todoData.taskName,
id: getId()

})
setTodoInLocalStorage()
}

const setTodoInLocalStorage=()=>{
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

const deleteOneTodo=(id)=>{
todos.value= todos.value.filter((todo)=>todo.id !== id)
toast.success('Tâche supprimée avec succés')
if(todos.value.length ===0){
  toast.warning("Tu n'as plus de tâche")
}
setTodoInLocalStorage()

}
</script>

<style scoped>


</style>
