<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['mode']
}
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #008060;
  border: 1px solid #008060;
  color: white;
  cursor: pointer;
  border-radius: 4px;
}

button:hover,
button:active {
  background-color: #004c3f;
  border-color: #004c3f;
}

.flat {
  background-color: transparent;
  color: #004c3f;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #a5cfc8;
}
</style>
