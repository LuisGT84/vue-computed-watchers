<script setup>
import { ref } from 'vue'
import WelcomeComputed from './components/WelcomeComputed.vue'
import HelloReverse from './components/HelloReverse.vue'
import WatchYesNo from './components/WatchYesNo.vue'

const tab = ref('semana1')        // fijo en semana1
const view = ref('intro')         // intro | reverse | watcher
</script>

<template>
  <div class="container">
    <h1>Curso Vue.js — Computed & Watchers (Semana 1)</h1>

    <div class="nav">
      <button :class="{active: view==='intro'}"   @click="view='intro'">Introducción</button>
      <button :class="{active: view==='reverse'}" @click="view='reverse'">Prop. Computadas</button>
      <button :class="{active: view==='watcher'}" @click="view='watcher'">Watcher (sí/no)</button>
    </div>

    <div class="card" v-if="view==='intro'">
      <WelcomeComputed/>
      <hr>
      <p><small>Abrí la consola del navegador para comparar <b>computed</b> vs <b>método</b> (verás los <code>console.count</code>).</small></p>
    </div>

    <div class="card" v-else-if="view==='reverse'">
      <HelloReverse/>
      <p><small>Reproduce “Hola → aloH” usando una <b>propiedad computada</b> y la misma lógica como <b>método</b>.</small></p>
    </div>

    <div class="card" v-else>
      <WatchYesNo/>
      <p><small>Ejemplo de <b>watch</b> con <i>debounce</i> y llamada a API (yes/no).</small></p>
    </div>
  </div>
</template>
