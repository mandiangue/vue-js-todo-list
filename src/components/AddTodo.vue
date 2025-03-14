<template>
  <div class="container">
    <h2 class="header">My TodoList</h2>
    <div class="row">
      <div class="col-md">
        <form @submit.prevent="submitTask">
          <input type="text" class="form-control" placeholder="Ajouter une tâche" v-model="taskName">
          <button type="submit" class="btn btn-md btn-primary">Ajouter une tâche</button>

        </form>
        <div v-if="errorMessage" class="text-center error mt-4">{{ errorMessage }}</div>
      </div>
    </div>
  </div>

</template>
<script setup>

import { ref } from 'vue'



const taskName = ref('')
const errorMessage = ref(false)
const emitTodo = defineEmits(['todoEmitted'])

const submitTask = () => {
  if (!taskName.value) {
    errorMessage.value = 'Ce champ est requis'
    setTimeout(() => {
      errorMessage.value = ''
    }, 2000)
    return
  }

  const todoData = {
    taskName: taskName.value,

  }
  emitTodo('todoEmitted', todoData)
  taskName.value = ''
}
</script>

<style scoped>
.header {
  width: 700px;
  margin: auto;
  padding: 1rem;
  background-color: rgb(10, 43, 72);
  color: #fff;
  text-align: center;
}

form {
  width: 700px;
  margin: auto;
  display: flex;
  justify-content: center;
  margin-top: 2rem;

}

.btn {
  margin: .2rem;
}

form input {
  width: 400px;
  margin: .2rem;
}

.list {
  width: 100%;
  margin: 4rem auto;

}

.error {
  width: 200px;
  margin: 0 auto;
  padding: .5rem;
  color: rgb(255, 255, 255);
  background-color: rgb(249, 56, 8);
  border-radius: 5px;
}
</style>
