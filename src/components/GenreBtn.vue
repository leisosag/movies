<template>
  <button @click="getGenre(genre.id, genre.name)" class="btn btn-genre mr-2">
    {{ genre.name }}
  </button>
</template>
<script>
export default {
  name: 'GenreBtn',
  props: {
    genre: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getGenre(id, name) {
      this.$emit('getGenre', id, name);
    },
  },
};
</script>
<style>
.btn-genre {
  background-color: transparent;
  border: 1px solid var(--white);
  color: var(--white);
  border-radius: 0;
  padding: 0.2rem 0.4rem;
  font-weight: 600;
}
.btn-genre:hover {
  border: 1px solid var(--red);
  color: var(--red);
}
</style>
