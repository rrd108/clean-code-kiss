<script setup lang="ts">
  import { computed, ref } from 'vue'

  const pass = ref('')

  const minLength = 6

  const strength = computed(() => {
    const result = { len: false, mixedCase: false, special: false }

    if (pass.value.length >= minLength) {
      result.len = true
    }

    if (pass.value.match(/[a-z]/) && pass.value.match(/[A-Z]/)) {
      result.mixedCase = true
    }

    if (pass.value.match(/[\d\W]/)) {
      result.special = true
    }

    return result
  })

  const isValid = computed(() => Object.values(strength.value).every(v => v))
</script>

<template>
  <main>
    <fieldset>
      <label>
        Új jelszó "2"
        <input type="text" v-model="pass" />
      </label>
    </fieldset>

    <ul>
      <li>
        <span>{{ strength.len ? '✅' : '❌' }}</span>
        minimum 6 karakter
      </li>
      <li>
        <span>{{ strength.mixedCase ? '✅' : '❌' }}</span>
        kis és nagybetű
      </li>
      <li>
        <span>{{ strength.special ? '✅' : '❌' }}</span>
        legalább 1 szám vagy 1 speciális karakter
      </li>
    </ul>

    <button type="submit" :disabled="!isValid">Ment</button>
  </main>
</template>

<style scoped></style>
