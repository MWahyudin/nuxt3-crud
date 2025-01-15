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
            <button @click="goToPost(post.id)">View</button>
            <button @click="goToEdit(post.id)">Edit</button>
            <button @click="confirmDelete(post.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '~/services/api';
import { useRouter } from 'vue-router';

const posts = ref([]);
const router = useRouter();

// Ambil data post
onMounted(async () => {
  const { data } = await api.get('/posts');
  posts.value = data;
});

// Fungsi navigasi ke halaman detail post
const goToPost = (id) => {
  router.push(`/posts/${id}`);
};

// Fungsi navigasi ke halaman edit post
const goToEdit = (id) => {
  router.push(`/posts/edit?id=${id}`);
};

// Fungsi navigasi ke halaman create post
const goToCreatePost = () => {
  router.push(`/posts/create`);
};

// Fungsi untuk menghapus post
const deletePost = async (id) => {
  await api.delete(`/posts/${id}`);
  alert('Post Deleted!');
  posts.value = posts.value.filter((post) => post.id !== id);
};

// Konfirmasi penghapusan
const confirmDelete = (id) => {
  const isConfirmed = window.confirm('Are you sure you want to delete this post?');
  if (isConfirmed) {
    deletePost(id);
  }
};
</script>
