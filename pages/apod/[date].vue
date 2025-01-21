<template>
    <div>
      <h1>{{ apod.title }}</h1>
      <img :src="apod.url" :alt="apod.title" />
      <p>{{ apod.explanation }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  const apod = ref({});
  const route = useRoute();
  const date = route.params.date;
  
  const fetchApodDetail = async () => {
    const response = await fetch(`https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY&date=${date}`);
    const data = await response.json();
    apod.value = data;
  };
  
  onMounted(fetchApodDetail);
  </script>
  