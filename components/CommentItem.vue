<template>
    <div class="comment-item">
      <h4>{{ comment.name }}</h4>
      <p>{{ comment.body }}</p>
      <p><strong>Email:</strong> {{ comment.email }}</p>
    </div>
  </template>
  
  <script setup>
  defineProps({
    comment: Object
  });
  </script>
  
  <style scoped>
  .comment-item {
    margin-bottom: 10px;
    border: 1px solid #eee;
    padding: 10px;
    border-radius: 5px;
    background-color: #f9f9f9;
  }
  </style>
  