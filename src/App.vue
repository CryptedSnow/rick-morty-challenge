<script setup>
  import CharacterTable from './components/CharacterTable.vue';
</script>

<template>
  <div class="container mx-auto p-6">
    <h1 class="text-3xl font-bold text-center mb-4">Rick and Morty - Characters </h1>
    <CharacterTable />
  </div>
</template>

<style scoped>
  .container {
    max-width: 1200px;
  }
</style>