<template>
    <div class="header">
        <img class="header__img" src="static/img/landing-page/header.png" alt="membre des forces de l'ordre">
        <div class="header__title">
            <div class="header__title--text">Old Not Obsolete</div>
            <border-text text="Couou"/>
        </div>
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

    &__title {
        position: fixed;
        top: 50%;
        left: 50%;
        z-index: 1;
        color: $white;
        display: flex;
        justify-content: center;
        align-items: center;
        font-family: $font-button;
        font-size: $font-size-xxxl;
        text-align: center;
        -webkit-text-stroke: 4px $black;
        transform: translate(-50%, -50%) skew(-45deg); // Combinez les transformations ici

        &--text {
            position: relative;
            display: inline-block;
            padding: 10px 20px; // Ajustez selon vos besoins
            overflow: hidden; // Cache les parties des pseudo-éléments qui dépassent

            &::before,
            &::after {
                content: "";
                position: absolute;
                width: 100%;
                height: 100%;
                border: 2px solid $white;
            }

            &::before {
                clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%, 4% 90%, 90% 4%);
                z-index: -1;
            }

            &::after {
                clip-path: polygon(10% 0, 100% 0, 96% 10%, 0 100%, 0 0);
                z-index: -2;
            }
        }
    }

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
    box-shadow: 100px 4px 8px 10px rgba(0, 0, 0, 0.2);
}

.white {
    background-color: white;
    position: relative;
    z-index: 3;
}
</style>
