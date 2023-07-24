<template>
  <header>
    <nav class="nav">
      <ul class="nav_ul">
        <li><a class="nav_link" href="#">Accueil</a></li>
        <li><a class="nav_link" href="#">Roster</a></li>
        <li><a class="nav_link" href="#">Contact</a></li>
        <Button @click="handleClick">Mon Bouton</Button>
      </ul>
    </nav>
    <header-logo title="h1"/>
  </header>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
.nav {
  &_ul {
    list-style: none;
    display: flex;
    gap: $spacing-m;
    background-color: $dark-gray;
    color: white;
    margin: 0;
    padding: $spacing-m;
    justify-content: flex-end;
    position: fixed; /* Modifier la valeur en "fixed" */
    top: 0; /* Pour ancrer la barre de navigation en haut de la page */
    left: 0; /* Pour ancrer la barre de navigation complètement à gauche */
    width: 100%; /* Pour occuper toute la largeur de l'écran */
  }

  &_link {
    color: $white;
    text-decoration: none;
  }
}
</style>
