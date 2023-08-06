<template>
    <div class="header">
        <img class="header__img" src="static/img/landing-page/header.png" alt="membre des forces de l'ordre">
        <div class="header__spacer"></div>
    </div>
    <div class="scrollable-content"></div>
    <div class="scrollable-content white"></div>
    <WidgetsDiscord />
</template>

<script setup lang='ts'>
    // Vous pouvez ajouter des comportements personnalisés ici si nécessaire.
</script>

<style lang='scss' scoped>
body {
  scroll-behavior: smooth;
}
.header {
    position: relative;
    width: 100%;
    height: 100vh;

    &__img {
        position: fixed;
        width: 100%;
        height: 100vh;
        object-fit: cover;
        object-position: center;
        z-index: 0;
    }

    &__spacer {
        height: 100vh;
    }
}

.scrollable-content {
    position: sticky;
    width: 100%;
    height: 150vh;
    background-color: $background-color;
    clip-path: polygon(22% 3%, 40% 3%, 44% 6%, 72% 6%, 76% 2%, 100% 2%, 100% 100%, 0 100%, 0 0, 19% 0);
    top: -150px;
    z-index: 2;
    box-shadow: 100px 4px 8px 10px rgba(0,0,0,0.2);
}

.white {
    background-color: white;
    position: relative;
    z-index: 3;
}
</style>
