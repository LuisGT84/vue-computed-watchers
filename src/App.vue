<script setup>
import { ref } from 'vue'
import WelcomeComputed from './components/WelcomeComputed.vue'
import HelloReverse from './components/HelloReverse.vue'
import WatchYesNo from './components/WatchYesNo.vue'
import TodoList from './components/todos/TodoList.vue'

const tab = ref('semana1')        // semana1 | semana2
const week1View = ref('intro')    // intro | reverse | watcher
</script>

<template>
  <div class="container">
    <h1>Curso Vue.js — Computed & Watchers</h1>
    <div class="nav">
      <button :class="{active: tab==='semana1'}" @click="tab='semana1'">Semana 1 — Fundamentos</button>
      <button :class="{active: tab==='semana2'}" @click="tab='semana2'">Semana 2 — Proyecto final</button>
    </div>

    <!-- SEMANA 1 -->
    <section v-if="tab==='semana1'">
      <div class="card">
        <div class="nav">
          <button :class="{active: week1View==='intro'}"   @click="week1View='intro'">Introducción</button>
          <button :class="{active: week1View==='reverse'}" @click="week1View='reverse'">Prop. Computadas</button>
          <button :class="{active: week1View==='watcher'}" @click="week1View='watcher'">Watcher (sí/no)</button>
        </div>

        <div v-if="week1View==='intro'">
          <WelcomeComputed/>
        </div>

        <div v-else-if="week1View==='reverse'">
          <HelloReverse/>
        </div>

        <div v-else>
          <WatchYesNo/>
        </div>
      </div>
    </section>

    <!-- SEMANA 2 -->
    <section v-else>
      <div class="card">
        <h2>Proyecto final — Lista de tareas</h2>
        <TodoList/>
      </div>
    </section>
  </div>
</template>
