<template>
  <div>
    <h1>Create Post</h1>
    <form @submit.prevent="createPost" class="form-horizontal">
      <div class="form-group">
        <label for="title" class="label">Title:</label>
        <input
          id="title"
          v-model="title"
          type="text"
          placeholder="Enter title"
          class="input-field"
          required
        />
      </div>
      
      <div class="form-group">
        <label for="body" class="label">Body:</label>
        <textarea
          id="body"
          v-model="body"
          placeholder="Enter body"
          class="input-field"
          required
        ></textarea>
      </div>
      
      <button type="submit" class="submit-btn">Submit</button>
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
  