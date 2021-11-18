<template>
  <div class="search">
    <input type="text" placeholder="Inserisci Titolo" v-model="title" />
    <button @click="$emit('search-film', title)">Search</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
    };
  },
};
</script>

<style>
</style>