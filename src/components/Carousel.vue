<template>
  <div id="carousel" class="carousel slide" data-ride="carousel">
    <ol class="carousel-indicators">
      <li data-target="#carousel" data-slide-to="0" class="active"></li>
      <li data-target="#carousel" data-slide-to="1"></li>
      <li data-target="#carousel" data-slide-to="2"></li>
    </ol>
    <div class="carousel-inner header-img">
      <!-- first slide -->
      <div class="carousel-item active">
        <picture>
          <source
            media="(min-width:401px)"
            srcset="../assets/icarealot-big.jpg"
          />
          <source
            media="(max-width:400px)"
            srcset="../assets/icarealot-tall.jpg"
          />
          <img src="../assets/icarealot-small.jpg" alt="i care a lot poster" />
        </picture>
        <div class="carousel-caption d-none d-md-block">
          <h2>I Care a Lot</h2>
          <p>
            A crooked legal guardian who drains the savings of her elderly wards
            meets her match when a woman she tries to swindle turns out to be
            more than she first appears.
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
      <!-- second slide -->
      <div class="carousel-item">
        <picture>
          <source media="(min-width:401px)" srcset="../assets/raya-big.jpg" />
          <source media="(max-width:400px)" srcset="../assets/raya-tall.jpg" />
          <img src="../assets/raya-small.jpg" alt="raya poster" />
        </picture>
        <div class="carousel-caption d-none d-md-block">
          <h2>Raya and the Last Dragon</h2>
          <p>
            In a realm known as Kumandra, a re-imagined Earth inhabited by an
            ancient civilization, a warrior named Raya is determined to find the
            last dragon.
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
      <!-- third slide -->
      <div class="carousel-item">
        <picture>
          <source media="(min-width:401px)" srcset="../assets/tenet-big.jpg" />
          <source media="(max-width:400px)" srcset="../assets/tenet-tall.jpg" />
          <img src="../assets/tenet-small.jpg" alt="tenet poster" />
        </picture>
        <div class="carousel-caption d-none d-md-block">
          <h2>Tenet</h2>
          <p>
            Armed with only one word, Tenet, and fighting for the survival of
            the entire world, a Protagonist journeys through a twilight world of
            international espionage on a mission that will unfold in something
            beyond real time.
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
    <a
      class="carousel-control-prev"
      href="#carousel"
      role="button"
      data-slide="prev"
    >
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a
      class="carousel-control-next"
      href="#carousel"
      role="button"
      data-slide="next"
    >
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
</template>
<script>
export default {
  name: 'Carousel',
};
</script>

<style>
.header-img img {
  width: 100%;
  height: 90vh;
  display: block;
  overflow: hidden;
  object-fit: cover;
}
.carousel-inner {
  z-index: 0;
}
.carousel-item img {
  width: 100%;
  height: 100vh;
  display: block;
  overflow: hidden;
  object-fit: cover;
}
.carousel-caption {
  top: 35%;
  text-align: left;
  width: 45vw;
  height: 45vh;
  padding: 1rem;
  background-color: var(--bgdark-transparent);
}
.carousel-caption h2 {
  font-size: 3rem;
  font-weight: 600;
  text-transform: uppercase;
  margin-bottom: 2rem;
  color: var(--black);
  color: var(--white);
}
@media screen and (min-width: 1400px) {
  .carousel-caption {
    height: 16rem;
  }
}
</style>
