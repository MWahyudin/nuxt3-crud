<template>
  <div>
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    <h2>Comments</h2>
    <div v-for="comment in comments" :key="comment.id">
      <CommentItem :comment="comment" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '~/services/api';
import { useRoute } from 'vue-router';
import CommentItem from '~/components/CommentItem.vue';

const route = useRoute();
const post = ref({});
const comments = ref([]);

onMounted(async () => {
  const { data } = await api.get(`/posts/${route.params.id}`);
  post.value = data;

  const { data: commentsData } = await api.get(`/posts/${route.params.id}/comments`);
  comments.value = commentsData;

});
</script>
