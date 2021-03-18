<template>
  <button class="btn btn-genre mr-2">{{ genre }}</button>
</template>
<script>
export default {
  name: 'GenreBtn',
  props: {
    genre: {
      type: String,
      required: true,
    },
  },
};
</script>
<style>
.btn-genre {
  background-color: var(--red);
  color: var(--white);
  border-radius: 2rem;
  padding-bottom: 0.6rem;
  font-size: 0.8rem;
}
</style>
