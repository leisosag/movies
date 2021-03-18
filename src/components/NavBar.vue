<template>
  <div id="navabar">
    <div class="container">
      <nav class="navbar navbar-expand-lg navbar-dark">
        <a class="navbar-brand" href="/">
          <img
            src="../assets/logo2.png"
            width="30"
            height="30"
            class="d-inline-block align-top mr-1"
            alt=""
          />
          MoviesDB
        </a>
      </nav>
    </div>
  </div>
</template>
<script>
export default {
  name: 'NavBar',
};
</script>
<style>
#navbar {
  background-color: var(--bgdark);
  min-height: 10vh;
  width: 100%;
}
</style>
