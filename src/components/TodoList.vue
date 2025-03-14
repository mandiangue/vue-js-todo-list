<template>

  <div class="text-center fs-4 m-4" v-if="todos.length > 0">Vous avez <span class="badge text-bg-danger"> {{
    todos.length }} </span> tâche(s) à faire.</div>
  <ul>

    <TransitionGroup name="animList">

      <li v-for="todo in todos" :key="todo.id">

        {{ todo.taskName }}
        <span class="date">{{ formateDate }}</span>
        <span @click.prevent="finirTache(todo.id)" class="remove">X</span>
      </li>

    </TransitionGroup>
  </ul>


</template>


<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  todos: {
    type: Array,
    required: true
  },
})
const currentDate = ref(new Date())
const listLi = ref([])
listLi.value = props.todos
const dateJour = currentDate.value.getDate()
const mois = currentDate.value.getMonth() + 1
const annee = currentDate.value.getFullYear()

const formateDate = computed(() => {
  if (dateJour && mois < 10) {
    return `${dateJour}-0${mois}-${annee}`
  }
  return `${dateJour}-${mois}-${annee}`
})

const emitDeleteTodo = defineEmits(['todoDeleted'])

const finirTache = (id) => {
  emitDeleteTodo('todoDeleted', id)
}

</script>

<style scoped>
ul {
  position: relative;
  margin-top: 3rem;
}

.date {
  position: absolute;
  left: 0;
  top: 5px;
  display: block;
  color: #fff;
  padding: .5rem;
  background-color: rgb(13, 61, 234);
  box-shadow: 2px 2px 2px #a1a0a0;
}

.remove {
  display: flex;
  position: absolute;
  top: 7px;
  right: 8px;
  font-size: .8rem;
  justify-content: center;
  align-items: center;
  text-align: center;
  cursor: pointer;
  width: 30px;
  height: 30px;
  background-color: rgb(232, 22, 22);
  border-radius: 50%;
  color: #fff;
  opacity: .5;
}

.remove:hover {
  opacity: 1.5;
  transition: background-color .2s;
  cursor: pointer;
}

ul li {
  width: 700px;
  box-shadow: 2px 2px 2px #e3e2e2;
  margin: .5rem auto;
  list-style: none;
  padding: .7rem;
  position: relative;
  text-align: center;

}

.animList-enter-from {
  opacity: 0;
  rotate: 60deg;
}

.animList-enter-to {
  opacity: 1;
  rotate: 0deg;
}

.animList-enter-active {
  transition: all 0.7s;
}

.animList-leave-active {
  opacity: 0;
  rotate: 60deg;
  transition: all 0.3s;
}
</style>