<script setup lang="ts">
  import { computed, ref } from 'vue'
  import Pass1 from './components/Pass1.vue'
  import Pass2 from './components/Pass2.vue'
  import Pass3 from './components/Pass3.vue'

  const page = ref(1)
  const components = [Pass1, Pass2, Pass3]
  const activeComponent = computed(() => components[page.value - 1])
</script>

<template>
  <nav>
    <span v-for="i in components.length" :key="i" @click="page = i">
      {{ i }}
    </span>
  </nav>

  <Transition name="slip" mode="out-in">
    <component :is="activeComponent" :page="page" />
  </Transition>
</template>

<style>
  nav span {
    margin: 0.5em;
    cursor: pointer;
    background-color: #3b3b3b;
    width: 1.5rem;
    display: inline-block;
  }
  main {
    display: grid;
    place-items: center;
    align-content: center;
    gap: 1em;
    background-color: #3b3b3b;
    color: #fff;
    padding: 2em;
    border-radius: 0.5em;
    overflow: hidden;
    max-width: 40em;
  }
  fieldset,
  input {
    font-size: 2rem;
  }
  fieldset {
    border: none;
    padding: 0;
    margin: 0;
  }
  label {
    font-weight: bold;
  }
  input {
    display: block;
    border: none;
    border-radius: 0.5em;
    padding: 0.5em;
    background-color: #fff;
    color: #3b3b3b;
    margin: 1em;
  }
  ul {
    list-style: none;
    text-align: left;
    font-size: 1.5rem;
  }

  .slip-enter-active,
  .slip-leave-active {
    transition: rotate 300ms ease-in-out;
    transform-origin: bottom left;
  }

  .slip-enter-from,
  .slip-leave-to {
    rotate: 122deg;
  }
</style>
