<template>
<div class="w-full h-full no-print">
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup>
useHead({
  title: "Buckhain's portfolio",
  meta: [
    { name: 'description', content: 'Portfolio' }
  ],
  htmlAttrs: {
    lang: 'en'
  }
})
</script>