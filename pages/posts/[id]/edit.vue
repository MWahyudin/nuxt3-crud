<template>
  <div>
    <h1>Edit Post</h1>
    <form @submit.prevent="updatePost">
      <label>Title:</label>
      <input v-model="title" required />
      <label>Body:</label>
      <textarea v-model="body" required></textarea>
      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '~/services/api';
import { useRoute } from 'vue-router';

const route = useRoute();
const title = ref('');
const body = ref('');

onMounted(async () => {
  const { data } = await api.get(`/posts/${route.params.id}`);
  title.value = data.title;
  body.value = data.body;
});

const updatePost = async () => {
  await api.put(`/posts/${route.params.id}`, { title: title.value, body: body.value });
  alert('Post Updated!');
};
</script>
