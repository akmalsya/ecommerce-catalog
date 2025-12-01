<template>
  <div>
    <button @click="$emit('prev')">Prev</button>
    <button @click="$emit('next')">Next</button>
    <button @click="$emit('random')">Random</button>
  </div>
</template>

<script>
export default { name:"Controls" }
</script>
