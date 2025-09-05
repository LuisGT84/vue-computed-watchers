<script setup>
import { ref, computed, onMounted, watch } from 'vue'
import TodoItem from './TodoItem.vue'

const STORAGE_KEY = 'todos-vue'
const todos = ref([])
const newText = ref('')
const filter = ref('todas') // todas | pendientes | completadas

onMounted(() => {
  const saved = localStorage.getItem(STORAGE_KEY)
  todos.value = saved ? JSON.parse(saved) : [
    { id:1, text:'Repasar computed vs methods', done:true },
    { id:2, text:'Implementar watcher con debounce', done:true },
    { id:3, text:'Terminar to-do list con localStorage', done:false },
  ]
})

watch(todos, (val) => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(val))
}, { deep:true })

function addTodo(){
  const t = newText.value.trim()
  if(!t) return
  todos.value.push({ id: Date.now(), text:t, done:false })
  newText.value = ''
}

function toggleTodo(id){
  const i = todos.value.findIndex(t => t.id===id)
  if(i>-1) todos.value[i].done = !todos.value[i].done
}

function removeTodo(id){
  todos.value = todos.value.filter(t => t.id!==id)
}

function clearCompleted(){
  todos.value = todos.value.filter(t => !t.done)
}

const total = computed(() => todos.value.length)
const completadas = computed(() => todos.value.filter(t => t.done).length)
const pendientes = computed(() => total.value - completadas.value)

const visibles = computed(() => {
  if (filter.value==='pendientes') return todos.value.filter(t => !t.done)
  if (filter.value==='completadas') return todos.value.filter(t => t.done)
  return todos.value
})
</script>

<template>
  <div class="gap" style="align-items:center; justify-content:space-between">
    <div class="gap">
      <span class="badge">Total: {{ total }}</span>
      <span class="badge">Completadas: {{ completadas }}</span>
      <span class="badge">Pendientes: {{ pendientes }}</span>
    </div>
    <div class="gap">
      <button class="btn" :class="{active: filter==='todas'}" @click="filter='todas'">Todas</button>
      <button class="btn" :class="{active: filter==='pendientes'}" @click="filter='pendientes'">Pendientes</button>
      <button class="btn" :class="{active: filter==='completadas'}" @click="filter='completadas'">Completadas</button>
    </div>
  </div>

  <div class="card">
    <div class="gap">
      <input type="text" v-model="newText" placeholder="Nueva tarea… (Enter para agregar)" @keyup.enter="addTodo">
      <button class="btn" @click="addTodo">Agregar</button>
      <button class="btn" @click="clearCompleted">Limpiar completadas</button>
    </div>

    <ul class="list">
      <TodoItem v-for="t in visibles" :key="t.id" :todo="t"
        @toggle="toggleTodo" @remove="removeTodo"/>
    </ul>

    <p v-if="!todos.length"><small>No hay tareas. ¡Agrega la primera!</small></p>
  </div>

  <p><small>
    Demostraciones: <b>listas</b> (v-for), <b>clases dinámicas</b>, <b>condicionales</b> (v-if),
    <b>eventos</b>, <b>v-model</b>, <b>componentes</b>, <b>computed</b> (contadores),
    y <b>watch</b> (persistencia en <code>localStorage</code>).
  </small></p>
</template>
