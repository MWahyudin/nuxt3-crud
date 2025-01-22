<template>
  <div>
    <h1>Fakta Angka</h1>
    <p>{{ fact.number }}: {{ fact.text }}</p>
    <button @click="deleteFact">Hapus Fakta</button>
    <button @click="editFact">Edit Fakta</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const fact = ref({});
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

const editFact = async () => {
  const newNumber = prompt('Masukkan angka baru untuk fakta:', fact.value.number);
  if (newNumber) {
    const res = await fetch(`http://numbersapi.com/${newNumber}`);
    const text = await res.text();
    fact.value = { number: newNumber, text };
  }
};

const deleteFact = () => {
  const confirmDelete = confirm('Apakah Anda yakin ingin menghapus fakta ini?');
  if (confirmDelete) {
    router.push('/'); // Redirect ke halaman utama setelah dihapus
  }
};
</script>
