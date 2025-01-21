<template>
  <div>
    <h1>Edit Fakta Angka</h1>
    <form @submit.prevent="updateFact">
      <label for="number">Angka:</label>
      <input v-model="fact.number" id="number" type="number" required />
      
      <label for="text">Fakta:</label>
      <textarea v-model="fact.text" id="text" required></textarea>
      
      <button type="submit">Update Fakta</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const fact = ref({ number: '', text: '' });
const route = useRoute();
const router = useRouter();

onMounted(async () => {
  await fetchFact();
});

const fetchFact = async () => {
  const number = route.params.id;
  const res = await fetch(`http://numbersapi.com/${number}`);
  const text = await res.text();
  fact.value = { number, text };
};

const updateFact = async () => {
  const res = await fetch(`http://numbersapi.com/${fact.value.number}`);
  const text = await res.text();
  fact.value.text = text; // Update fakta jika berhasil
  alert('Fakta berhasil diperbarui!');
  router.push(`/posts/${fact.value.number}`);
};
</script>
