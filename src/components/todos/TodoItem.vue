<script setup>
const props = defineProps({
  todo: { type:Object, required:true }
})
const emit = defineEmits(['toggle','remove'])
</script>

<template>
  <li class="item" :class="{done: todo.done}">
    <input type="checkbox" :checked="todo.done" @change="emit('toggle', todo.id)">
    <span style="flex:1">{{ todo.text }}</span>
    <button class="btn" @click="emit('remove', todo.id)">Eliminar</button>
  </li>
</template>
