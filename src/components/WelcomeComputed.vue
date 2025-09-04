<script setup>
import { ref, computed } from 'vue'

const nombre = ref('')
const saludoComputado = computed(() => {
  console.count('Recalcula saludoComputado')
  return nombre.value.trim()
    ? `¡Bienvenido/a, ${nombre.value.trim()}!`
    : 'Escribe tu nombre arriba…'
})

function saludoMetodo(){
  console.count('Ejecuta saludoMetodo()')
  return nombre.value.trim()
    ? `¡Bienvenido/a, ${nombre.value.trim()}!`
    : 'Escribe tu nombre arriba…'
}
</script>

<template>
  <h2>Bienvenida dinámica (computed vs método)</h2>
  <input type="text" v-model="nombre" placeholder="Tu nombre…">

  <div class="card">
    <p><b>Con propiedad computada:</b> {{ saludoComputado }}</p>
    <p><b>Con método:</b> {{ saludoMetodo() }}</p>
    <small>💡 La computada se cachea; el método se ejecuta en cada render.</small>
  </div>
</template>
