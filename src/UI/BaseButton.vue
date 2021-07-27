<template>
  <button :type="type" :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['type', 'mode']
};
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  margin-right: 0.2rem;
  background-color: #6d09ca;
  border: 1px solid #ffffff;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #7f2fe7;
  border-color: #ffffff;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #7f2fe7;
}
</style>
