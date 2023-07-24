<script setup lang="ts">
  import { computed, ref } from 'vue'

  const pass = ref('')

  const strength = computed(() => ({
    len: isLongEnough.value,
    mixedCase: hasMixedCase.value,
    numSpecial: hasNumber.value || hasSpecial.value,
  }))

  const minLength = 6

  const isLongEnough = computed(() => pass.value.length >= minLength)

  const hasMixedCase = computed(() =>
    Boolean(pass.value.match(/[a-z]/) && pass.value.match(/[A-Z]/))
  )

  const hasNumber = computed(() => Boolean(pass.value.match(/[\d]/)))

  const hasSpecial = computed(() => Boolean(pass.value.match(/[\W]/)))

  const isValid = computed(() => Object.values(strength.value).every(v => v))
</script>

<template>
  <main>
    <fieldset>
      <label>
        Új jelszó "3"
        <input type="text" v-model="pass" />
      </label>
    </fieldset>

    <ul>
      <li>
        <span>{{ strength.len ? '✅' : '❌' }}</span>
        minimum {{ minLength }} karakter
      </li>
      <li>
        <span>{{ strength.mixedCase ? '✅' : '❌' }}</span>
        kis és nagybetű
      </li>
      <li>
        <span>{{ strength.numSpecial ? '✅' : '❌' }}</span>
        legalább 1 szám vagy 1 speciális karakter
      </li>
    </ul>

    <button type="submit" :disabled="!isValid">Ment</button>
  </main>
</template>

<style scoped></style>
