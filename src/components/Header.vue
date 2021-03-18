<template>
  <div id="header">
    <div class="header-img">
      <picture>
        <source
          media="(min-width:401px)"
          srcset="../assets/background-big.jpg"
        />
        <source
          media="(max-width:400px)"
          srcset="../assets/background-tall.jpg"
        />
        <img src="../assets/background-small.jpg" />
      </picture>
      <div class="header-text container">
        <h1 class="text-white">I Care a Lot</h1>
        <h2 class="text-white">
          It is a long established fact that a reader will be distracted by the
          readable.
        </h2>
        <p class="text-white">
          The point of using Lorem Ipsum is that it has a more-or-less normal
          distribution of letters, as opposed to using 'Content here, content
          here'.
        </p>
        <a href="#">
          <button class="btn btn-danger">
            <i class="fas fa-caret-right mr-2"></i>Ver más
          </button>
        </a>
        <a href="#">
          <button class="ml-3 btn btn-outline-light">
            <i class="fas fa-plus mr-2"></i>Mi lista
          </button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style>
.header-img img {
  width: 100%;
  height: 100vh;
  display: block;
  overflow: hidden;
  object-fit: cover;
}
.header-text {
  position: absolute;
  text-align: left;
  bottom: 30%;
  right: 12%;
  z-index: 1;
}
.header-text h1 {
  font-size: 5rem;
  line-height: 5rem;
}
.header-text h2 {
  font-size: 1.5rem;
  width: 40vw;
}
.header-text p {
  font-size: 1rem;
  width: 40vw;
}
</style>
