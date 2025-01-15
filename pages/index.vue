<template>
    <div>
      <h1>Posts</h1>
      <nuxt-link to="/posts/create">Create New Post</nuxt-link>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Title</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.id }}</td>
            <td>{{ post.title }}</td>
            <td>
              <nuxt-link :to="`/posts/${post.id}`">View</nuxt-link>
              <nuxt-link :to="`/posts/${post.id}/edit`">Edit</nuxt-link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import api from '~/services/api';
  
  const posts = ref([]);
  
  onMounted(async () => {
    const { data } = await api.get('/posts');
    posts.value = data;
  });
  </script>
  