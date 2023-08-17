<template>
  <div class="graphCirc">
    <div class="graphCirc__text">{{ props.display }}</div>
    <svg width="100" height="100" viewBox="0 0 42 42" class="donut">
      <circle class="donut-hole" cx="21" cy="21" r="15.91549430918954"></circle>
      <circle class="donut-ring" cx="21" cy="21" r="15.91549430918954" fill="transparent" stroke-width="2.5"></circle>
      <circle class="donut-segment" cx="21" cy="21" r="15.91549430918954" fill="transparent" stroke-width="2.5"
        v-bind:style="segmentStyle"></circle>
      <text x="21" y="21" alignment-baseline="middle" text-anchor="middle">{{ props.value }}%</text>
    </svg>
  </div>
</template>

<script setup lang='ts'>

const props = defineProps({
  display: {
    type: String,
    required: true
  },
  value: {
    type: String,
    required: true
  }
});

const segmentStyle = computed(() => {
  const circumference = 100;
  const segmentLength = (circumference * props.value) / 100;
  const gapLength = circumference - segmentLength;
  return { 'stroke-dasharray': `${segmentLength} ${gapLength}` };
});


</script>

<style lang='scss' scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.graphCirc {
  display: flex;
  flex-direction: column; // empile les éléments verticalement
  align-items: center; // centre les éléments horizontalement

  &__text {
    color: $secondary-color;
    font-family: $font-main;
    font-size: $font-size-base;
    width: 200px; 
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
}

.donut {
  width: 100%;
  height: 100%;
  max-width: 200px;
  max-height: 200px;
  margin: 0 auto 20px auto;
  transform: rotate(-90deg);
  display: block;
  border: none;
  outline: none;
  background: none;
  flex: 0 0 100px;
  margin: 0;
  padding: 0;

  &-hole {
    fill: $black
  }

  &-ring {
    stroke: $light-gray;
  }

  &-segment {
    stroke: $secondary-color;
  }

}

text {
  color: $secondary-color;
  transform-origin: 21px 21px;
  transform: rotate(90deg);
  font-size: $font-size-xs;
  /* Réduisez la taille de la police selon vos préférences. */
  dy: 0.3em;
  /* Ajustement pour centrer verticalement le texte. */
}

</style>