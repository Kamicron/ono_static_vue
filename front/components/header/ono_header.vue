<template>
  <header>
    <nav class="nav">
      <ul class="nav__ul">
        <li><a class="nav__ul--link" href="#">Accueil</a></li>
        <li><a class="nav__ul--link" href="#">Roster</a></li>
        <li><a class="nav__ul--link" href="#">Contact</a></li>
      </ul>
    </nav>
    <!-- <header-logo title="h1"/> -->
  </header>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
header {
  background-color: white;
  position: fixed;
  z-index: 100;
  width: 500px;
  margin-right: 500px;
  clip-path: polygon(0 0, 100% 0%, 85% 100%, 0% 100%);
  box-shadow: 20px 20px 20px red;

  .nav {
    &__ul {
      display: flex;
      gap: $spacing-m;

      &--link {
        color: $background-color;
        text-decoration: none;
      }
    }
  }
}
</style>
