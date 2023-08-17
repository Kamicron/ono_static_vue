<template>
  <div class="horizontal-bar-graph">
    <p class="horizontal-bar-graph__label">{{ text }}</p>
    <div class="horizontal-bar-graph__container">
      <div class="horizontal-bar-graph__bar" :style="{ width: `${value}%` }"></div>
      <span class="horizontal-bar-graph__percentage">{{ value }}%</span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, toRefs, defineProps } from 'vue';

const props = defineProps({
  value: String,
  text: String,
});

const { value, text } = toRefs(props);
</script>

<style lang="scss" scoped>
.horizontal-bar-graph {
  width: 100%;

  &__label {
    font-family: $font-main;
    font-size: $font-size-sm;
    font-weight: $font-weight-medium;
    line-height: $line-height-base;
    margin-bottom: $spacing-xs;
    color: $white;
    text-align: start;
  }

  &__container {
    background-color: $medium-gray;
    position: relative;
    width: 100%;
    height: $spacing-m; // Ajustez ceci en fonction de la hauteur désirée pour la barre graphique
  }

  &__bar {
    background-color: $main-color;
    height: 100%; // Cela permettra d'ajuster la barre à la hauteur de son conteneur
    transition: width 0.3s ease-out;
  }

  &__percentage {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: $white;
    font-family: $font-main;
    font-size: $font-size-sm;
    font-weight: $font-weight-medium;
    z-index: 1; // Assurez-vous que le pourcentage est au-dessus de la barre graphique
  }
}
</style>