<script setup>
import WeaponsListView from '../components/WeaponsListView.vue';
import { ref } from 'vue';
let weapons = ref([]);
fetch("http://localhost:3001/api/weapons")
  .then(response => response.json())
  .then(data => weapons.value = data);
console.log("in HomeView: ", weapons);
</script>

<template>
  <WeaponsListView :weapons="weapons" />
</template>
