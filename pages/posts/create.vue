<template>
  <div>
    <h1>Tambah Gambar APOD Favorit</h1>
    <button @click="createApod">Tambah Gambar APOD Baru</button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

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
      let apodList = JSON.parse(localStorage.getItem('apodList')) || [];
      apodList.push(newApod);
      localStorage.setItem('apodList', JSON.stringify(apodList));
      router.push('/');
    } else {
      alert("Data tidak ditemukan!");
    }
  }
};
</script>
