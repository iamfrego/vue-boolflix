<template>
  <div class="search fixed_search d-flex">
    <input
      @keyup.enter="$emit('search-film', title)"
      type="text"
      placeholder="Inserisci Titolo"
      v-model="title"
      class="me-2"
    />
    <button @click="$emit('search-film', title)" class="btn btn-light">
      Search
    </button>
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
.fixed_search {
  position: fixed;
  top: 35px;
  right: 40px;
  z-index: 10000;
}
</style>