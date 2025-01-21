<template>
  <div>
    <h1>Daftar Gambar APOD Favorit</h1>
    <ul>
      <li v-for="(apod, index) in apodList" :key="index">
        <img :src="apod.url" :alt="apod.title" width="200" />
        <p>{{ apod.title }}</p>
        <button @click="deleteApod(index)">Hapus</button>
        <button @click="viewDetail(apod.date)">Lihat Detail</button>
      </li>
    </ul>
    <button @click="createApod">Tambah Gambar APOD Favorit</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const apodList = ref([]);

const fetchApods = async () => {
  // Ambil data APOD favorit dari storage atau API
  const storedApods = JSON.parse(localStorage.getItem('apodList')) || [];
  apodList.value = storedApods;
};

const createApod = async () => {
  const date = prompt("Masukkan tanggal (YYYY-MM-DD) untuk APOD:");
  if (date) {
    const response = await fetch(`https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY&date=${date}`);
    const data = await response.json();
    if (data) {
      const newApod = {
        date: date,
        title: data.title,
        url: data.url,
        explanation: data.explanation,
      };
      apodList.value.push(newApod);
      localStorage.setItem('apodList', JSON.stringify(apodList.value));
    } else {
      alert("Data tidak ditemukan!");
    }
  }
};

const deleteApod = (index) => {
  apodList.value.splice(index, 1);
  localStorage.setItem('apodList', JSON.stringify(apodList.value));
};

const viewDetail = (date) => {
  // Menggunakan router untuk menavigasi ke halaman detail berdasarkan tanggal
  router.push(`/apod/${date}`);
};

onMounted(fetchApods);
</script>
