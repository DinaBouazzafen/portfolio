<template>
    <div class="opacity-80 animate-fade animate-once animate-delay-[100ms] road-rage-regular">
      <div
      class="text-5xl font-bold road-rage-regular">
      {{ settings.site_title }}</div>
      <div class="text-4xl text-red-700 grenze">
      {{ settings.site_subtitle }}
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const settings = ref({});
  // Use useFetch to load the JSON data from the public folder
  const { data, error } = await useFetch('/_data/settings.json');
  
  // Set the data to the settings ref
  if (data.value) {
    settings.value = data.value;
  } else if (error.value) {
    console.error('Error loading settings:', error.value);
  }
  </script>