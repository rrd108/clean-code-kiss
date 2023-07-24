<script setup lang="ts">
  import { computed, ref } from 'vue'

  const pass = ref('')

  const strength = computed(() =>
    Boolean(pass.value.match(/(?=.*[a-z])(?=.*[A-Z])(?=.*[\d\W]).{6,}/))
  )
</script>

<template>
  <main>
    <fieldset>
      <label>
        Új jelszó "1" {{ strength ? '✅' : '❌' }}
        <input type="text" v-model="pass" />
      </label>
    </fieldset>

    <ul>
      <li>minimum 6 karakter</li>
      <li>kis és nagybetű</li>
      <li>legalább 1 szám vagy 1 speciális karakter</li>
    </ul>

    <button type="submit" :disabled="!strength">Ment</button>
  </main>
</template>

<style scoped></style>
