<!-- components/PostItem.vue -->
<template>
    <div class="post-item">
      <h3>{{ post.title }}</h3>
      <p>{{ post.body }}</p>
      <nuxt-link :to="`/posts/${post.id}`">Read More</nuxt-link>
    </div>
  </template>
  
  <script setup>
  defineProps({
    post: Object
  });
  </script>
  
  <style scoped>
  .post-item {
    margin-bottom: 30px;
  }
  </style>
  