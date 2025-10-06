<template>
  <div class="container">
    <h1>Gestor de tareas</h1>

  
    <input 
      v-model="newTask" 
      placeholder="Escribe la tarea aqui" 
      @keyup.enter="addTask" 
    />
    <button @click="addTask">Agregar</button>

    <hr />

    
    <div v-if="tasks.length === 0">
      <p>No hay tareas registradas</p>
    </div>

    
    <div v-else class="board">
    
      <div class="column">
        <h2>To Do</h2>
        <ul>
          <li v-for="tarea in tasks.filter(tarea => tarea.status === 'todo')" :key="tarea.id">
            {{ tarea.text }}
            <button @click="moveRight(tarea)">➡️</button>
          </li>
        </ul>
      </div>

      
      <div class="column">
        <h2>Doing</h2>
        <ul>
          <li v-for="tarea in tasks.filter(tarea => tarea.status === 'doing')" :key="tarea.id">
            {{ tarea.text }}
            <button @click="moveRight(tarea)">➡️</button>
          </li>
        </ul>
      </div>

      
      <div class="column">
        <h2>Done</h2>
        <ul>
          <li v-for="tarea in tasks.filter(tarea => tarea.status === 'done')" :key="tarea.id">
            {{ tarea.text }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

const newTask = ref("")
const tasks = ref([])
let idCounter = 0

const addTask = () => {
  const text = newTask.value.trim()
  if (text !== "") {
    tasks.value.push({ id: idCounter++, text, status: "todo" })
    newTask.value = ""
  }
}

const moveRight = (task) => {
  if (task.status === "todo") task.status = "doing"
  else if (task.status === "doing") task.status = "done"
}
</script>

<style scoped>
.container {
  max-width: 900px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
  text-align: center;
  color: #fff;
}

input {
  padding: 8px;
  width: 60%;
}

button {
  margin-left: 6px;
  padding: 4px 8px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

hr {
  margin: 20px 0;
  border: 1px solid #555;
}

.board {
  display: flex;
  margin-top: 20px;
  border-left: 2px dashed #aaa;
  border-right: 2px dashed #aaa;
}

.column {
  flex: 1;
  padding: 10px;
  border-left: 2px dashed #aaa;
}

.column:first-child {
  border-left: none;
}

h2 {
  margin-bottom: 10px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 12px;
  padding: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
