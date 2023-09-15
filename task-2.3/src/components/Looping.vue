<script setup>
defineProps({
  fruit: {
    type: String,
    required: true
  }
})
defineEmits(['emitAdd'])
</script>

<template>
<p>Hello, I have some {{ fruit }}</p>
<button @click="$emit('emitAdd')">Emit Custom Event</button>
<br>
<b><slot /></b>
</template>

<style scoped>

</style>
