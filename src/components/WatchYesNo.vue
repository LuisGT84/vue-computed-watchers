<script setup>
import { ref, watch } from 'vue'
import axios from 'axios'

function debounce(fn, wait=500){
  let t
  return (...args) => { clearTimeout(t); t = setTimeout(() => fn(...args), wait) }
}

const question = ref('')
const answer   = ref('No puedo darte una respuesta hasta que hagas una pregunta!!')

const debouncedGetAnswer = debounce(getAnswer, 500)

watch(question, () => {
  answer.value = 'Esperando que deje de escribir...'
  debouncedGetAnswer()
})

function capitalize(s){ return s ? s[0].toUpperCase()+s.slice(1) : s }

async function getAnswer(){
  if (!question.value.includes('?')){
    answer.value = 'Las preguntas suelen contener un signo de interrogación. ;-)'
    return
  }
  try{
    answer.value = 'Pensando...'
    const { data } = await axios.get('https://yesno.wtf/api')
    answer.value = capitalize(data.answer)
  }catch(e){
    answer.value = '¡Error! No se pudo alcanzar la API.'
  }
}
</script>

<template>
  <h2>Watcher — Pregunta de sí/no</h2>
  <div class="card">
    <p>Haz una pregunta de sí/no:</p>
    <input type="text" v-model="question" placeholder="¿Hoy lloverá?">
    <p style="margin-top:10px">{{ answer }}</p>
  </div>
</template>
