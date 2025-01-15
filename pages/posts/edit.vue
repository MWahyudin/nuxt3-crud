<template>
  <div>
    <h1>Edit Post</h1>
    <form @submit.prevent="updatePost">
      <label for="title">Title:</label>
      <input id="title" v-model="title" required />

      <label for="body">Body:</label>
      <textarea id="body" v-model="body" required></textarea>

      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '~/services/api';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const title = ref('');
const body = ref('');

// Ambil ID dari query parameter
const postId = route.query.id;

onMounted(async () => {
  if (postId) {
    try {
      const { data } = await api.get(`/posts/${postId}`);
      title.value = data.title;
      body.value = data.body;
    } catch (error) {
      console.error('Failed to fetch post data:', error);
      alert('Error loading post details.');
    }
  }
});

// Fungsi untuk mengupdate post
const updatePost = async () => {
  try {
    await api.put(`/posts/${postId}`, { title: title.value, body: body.value });
    alert('Post Updated!');
    router.push(`/posts/${postId}`);
  } catch (error) {
    console.error('Failed to update post:', error);
    alert('Error updating post.');
  }
};
</script>
