<template>
    <div>
      <h1>Create Post</h1>
      <form @submit.prevent="createPost">
        <label>Title:</label>
        <input v-model="title" required />
        <label>Body:</label>
        <textarea v-model="body" required></textarea>
        <button type="submit">Submit</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import api from '~/services/api';
  
  const title = ref('');
  const body = ref('');
  
  const createPost = async () => {
    const response = await api.post('/posts', { title: title.value, body: body.value });
    alert('Post Created: ' + response.data.id);
  };
  </script>
  