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
  import { useRouter } from 'vue-router';
  import api from '~/services/api';
  
  const title = ref('');
  const body = ref('');
  const router = useRouter();
  
const createPost = async () => {
  try {
    // Kirim data post baru ke API
    const response = await api.post('/posts', { title: title.value, body: body.value });
    
    // Setelah post berhasil dibuat, arahkan pengguna kembali ke halaman daftar post
    router.push('/');
    
    // Optional: Anda bisa memberi feedback seperti alert atau toast
    alert('Post Created: ' + response.data.id);
  } catch (error) {
    console.error("Error creating post:", error);
  }
};
  </script>
  