<template>
    <div>
      <h1>Comments for Post {{ post.id }}</h1>
      <ul>
        <li v-for="comment in comments" :key="comment.id">
          <strong>{{ comment.name }}</strong>: {{ comment.body }}
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import api from '~/services/api';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  const post = ref({});
  const comments = ref([]);
  
  onMounted(async () => {
    // Mengambil post berdasarkan ID
    const { data: postData } = await api.get(`/posts/${route.params.id}`);
    post.value = postData;
  
    // Mengambil komentar untuk post tersebut
    const { data: commentsData } = await api.get(`/posts/${route.params.id}/comments`);
    comments.value = commentsData;
  });
  </script>
  