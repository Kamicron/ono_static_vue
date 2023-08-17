<template>
  <div class="player__information">
    <div class="player__information-name">
      <h2 class="player__information-name--role">Team Elite</h2>
      <h3 class="player__information-name--pseudo">{{ playerData.pseudo }}</h3>
    </div>
    <img :src="playerData.playerImage" alt="Joueur" class="player__information-image" v-if="playerData.playerImage" />
  </div>
</template>

<script setup lang='ts'>
const props = defineProps({
  playerData: {
    type: Object,
    required: true,
    default: () => ({
      pseudo: '',
      playerImage: ''
    })
  },
})

</script>

<style lang='scss' scoped>
.player__information {
  background-color: $medium-gray;
  padding-bottom: $spacing-m;
  &-name {


    &--role {
      margin: 0;
      font-size: $font-size-xl;
      font-family: $font-button;
      text-transform: uppercase;
      font-weight: $font-weight-medium;
      color: $main-color;
    }

    &--pseudo {
      margin: 0;
      font-size: $font-size-xxl;
      font-family: $font-button;
      text-transform: uppercase;
      font-weight: $font-weight-medium;
      color: $secondary-color;
    }
  }

  &-image {
    width: 20%;
    height: auto;
    border-radius: 50%;
    margin-top: $spacing-m;
    border: 2px solid $background-color;
  }

}
</style>