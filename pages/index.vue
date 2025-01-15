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
              <button @click="deletePost(post.id)">Delete</button>
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

  const deletePost = async (id) => {
  await api.delete(`/posts/${id}`);
  alert('Post Deleted!');
  posts.value = posts.value.filter((post) => post.id !== id);
};

  
  onMounted(async () => {
    const { data } = await api.get('/posts');
    posts.value = data;
  });

  
// Fungsi untuk navigasi ke halaman post
const goToPost = (id) => {
  const router = useRouter();
  router.push(`/posts/${id}`); // Pindah ke halaman View Post
};

// Fungsi untuk navigasi ke halaman edit post
const goToEdit = (id) => {
  const router = useRouter();
  router.push(`/posts/${id}/edit`); // Pindah ke halaman Edit Post
};

// Fungsi untuk navigasi ke halaman Create Post
const goToCreatePost = () => {
  const router = useRouter();
  router.push(`/posts/create`); // Pindah ke halaman Create Post
};

// Konfirmasi penghapusan
const confirmDelete = (id) => {
  const isConfirmed = window.confirm('Are you sure you want to delete this post?');
  if (isConfirmed) {
    deletePost(id);
  }
};
  </script>
  