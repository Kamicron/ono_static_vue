<template>
  <div class="card">
    <div class="card__image">
      <img
        src="https://images.unsplash.com/photo-1604135307399-86c6ce0aba8e?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1374&q=80"
        alt="Image de l'article">
    </div>
    <div class="card__content card__content--hover"></div>
    <div class="card__content">
      <h3 class="card__content--title">Titre de l'article</h3>
      <p class="card__content--description">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor
        incididunt ut labore et dolore
        magna aliqua.</p>
      <a class="card__content--link" href="#">
        <border-text text="Voir plus" :fontSize="24" :borderWidth="3" color="white" hoverColor="light-dynamic" />
      </a>
    </div>
  </div>
</template>

<script setup lang='ts'>

</script>

<style lang='scss' scoped>
.card {
  position: relative;
  width: 300px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

  &__image {
    width: 100%;
    height: 200px;
    overflow: hidden;
    position: relative;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transform: scale(1.1);
    }
  }

  &__content {
    background-color: $main;
    color: #fff;
    padding: 20px;
    position: absolute;
    top: 150px;
    left: 20px;
    width: 260px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
    border-radius: 5px;
    transition: transform 0.3s ease-in-out;

    &--title {
      margin: 0 0 10px 0;
      color: $dynamic;
    }

    &--description {
      margin: 0 0 10px 0;
    }

    &--link {
      text-decoration: none;
    }
  }

  &__content--hover {
    background-color: $dynamic;
    height: 250px;
    z-index: 0;
  }

  &:hover {
    .card__content:not(.card__content--hover) {
      transform: translate(10px, -10px);
    }
  }
}
</style>
