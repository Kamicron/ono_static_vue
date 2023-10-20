<template>
  <div class="header-wrapper">
    <header ref="headerRef" :class="{ 'is-sticky': isSticky }">
      <nav class="nav">
        <ul class="nav__ul">
          <li>
            <a class="nav__ul--link" href="#">
              <border-text text="Acceuil" :fontSize="24" :borderWidth="3" color="white" hoverColor="light-dynamic" />
            </a>
          </li>
          <li>
            <a class="nav__ul--link" href="#">
              <border-text text="Roster" :fontSize="24" :borderWidth="3" color="white" hoverColor="light-dynamic" />
            </a>
          </li>
          <li>
            <a class="nav__ul--link" href="#">
              <border-text text="Contact" :fontSize="24" :borderWidth="3" color="white" hoverColor="light-dynamic" />
            </a>
          </li>
        </ul>
      </nav>
      <!-- <header-logo title="h1"/> -->
      <img src="/img/logo/logo_ono-colored-dark_bg.png" alt="logo de ONO, coloré pour fond noir" class="logo_ono">
    </header>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const headerRef = ref(null);
const isSticky = ref(false);

onMounted(() => {
  const initialTop = headerRef.value.offsetTop;
  const checkScroll = () => {
    if (window.pageYOffset >= initialTop) {
      isSticky.value = true;
    } else {
      isSticky.value = false;
    }
  };

  window.addEventListener('scroll', checkScroll);

  onUnmounted(() => {
    window.removeEventListener('scroll', checkScroll);
  });
});
</script>


<style lang="scss" scoped>
.header-wrapper {
  position: relative; // ou rien si vous ne voulez pas spécifier de position ici
  height: 0;
}

header {
  position: relative;
}

.logo_ono {
  position: absolute;
  top: 5px;
  right: 50px;
  z-index: 1;
  width: 75px;
  transform: skew(45deg); // Appliquer le skew inverse pour que le texte reste droit

}

header {

  &.is-sticky {
    position: fixed;
    top: 0;
    left: -150px;
    z-index: 1000; // pour le mettre au-dessus des autres éléments
    box-shadow: 20px 20px 20px rgba($light-main, 0.4); // 0.5 est le niveau d'opacité, vous pouvez le changer comme vous le souhaitez

  }

  // background-color: $dark-gray;
  background-color: $main;
  position: relative;
  width: 1000px;
  z-index: 100;
  left: -150px;
  top: 100px;
  padding-left: $spacing-xl;
  box-shadow: 20px 20px 20px rgba($light-main, 0.4); // 0.5 est le niveau d'opacité, vous pouvez le changer comme vous le souhaitez
  transform: skew(-45deg); // Appliquer le skew inverse pour que le texte reste droit
  padding: 20px 0;

  .is-fixed {
    top: 0 !important;
    position: fixed;
    transition: top 0.3s ease-in-out;
  }

  .nav {
    padding: 0 200px;

    &__ul {
      display: flex;
      gap: $spacing-m;
      list-style: none;
      padding: 0;
      justify-content: center;
      align-items: center;
      margin: 0;
      transform: skew(45deg); // Appliquer le skew inverse pour que le texte reste droit

      &--border {
        border: 2px solid $white;
        padding: 0 $spacing-l;
        margin: 20px 0;
        transform: skew(45deg); // Appliquer le skew à l'élément a pour créer le parallélogramme
        transition: border 0.3s ease-in-out;
      }

      li {
        overflow: hidden;
        position: relative;
        margin-right: 10px;

        a {
          color: $white;
          text-decoration: none;
          font-family: $font-button;
          font-size: $font-size-xl;
          letter-spacing: $letter-spacing-wide;
          font-weight: $font-weight-bold;
          transition: color 0.3s ease-in-out;

          &:hover {
            color: $secondary-color;
          }
        }

        &--link {
          display: block;
          padding: 10px 20px;
          text-decoration: none;
          color: white;

          &:before {
            content: "";
            display: block;
          }
        }
      }
    }
  }
}
</style>
