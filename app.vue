<script setup lang="ts">
const colorMode = useColorMode()
const toggleDark = () => colorMode.value = colorMode.value === 'light' ? 'dark' : 'light'

const validatorsStore = useValidatorsStore()
await callOnce(validatorsStore.fetchValidators)

const route = useRoute()
const validatorDetail = computed(() => !!route.params.address)
</script>

<template>
  <div flex="~ col gap-64" mx-auto size-screen max-h-screen max-w-1200 px-32 py-20>
    <header flex="~ gap-32 row items-center">
      <NuxtLink to="/" i-nimiq:logos-nimiq-horizontal ml-16 h-24 w-90 dark:i-nimiq:logos-nimiq-white-horizontal />
      <NuxtLink v-if="validatorDetail" to="/" block w-max arrow-back ghost-btn>
        Go Back
      </NuxtLink>
      <div flex-auto />
      <NuxtLink to="https://github.com/onmax/nimiq-validators" i-nimiq:logos-github-mono target="_blank" />
      <button i-nimiq:moon @click="() => toggleDark()" />
    </header>

    <main flex-1>
      <NuxtPage />
    </main>
  </div>
</template>
