<template>
    <div>
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import api from '~/services/api';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  const post = ref({});
  
  onMounted(async () => {
    const { data } = await api.get(`/posts/${route.params.id}`);
    post.value = data;
  });
  </script>
  