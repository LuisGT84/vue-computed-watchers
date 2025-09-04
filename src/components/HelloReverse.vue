<script setup>
import { ref, computed } from 'vue'

const message = ref('Hola')

const reversedMessage = computed(() => {
  console.count('Recalcula reversedMessage')
  return message.value.split('').reverse().join('')
})

function reverseMessage(){
  console.count('Ejecuta reverseMessage()')
  return message.value.split('').reverse().join('')
}
</script>

<template>
  <h2>Propiedades computadas — ejemplo básico</h2>
  <div class="card">
    <p>Mensaje original: "{{ message }}"</p>
    <p>Mensaje invertido computado: "{{ reversedMessage }}"</p>
    <hr>
    <p>La misma lógica con <b>método</b>: "{{ reverseMessage() }}"</p>
    <input type="text" v-model="message" placeholder="Escribe para probar…">
    <div class="badge">Resultado esperado: “Hola” → “aloH”</div>
  </div>
</template>
