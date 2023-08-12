<template>
<div class="discord">
  <div class="discord__wrapper">
    <p class="discord__wrapper--text">Discord</p>

    <img src="static/img/logo/discord.png" alt="Logo discord" width="50px">
  </div>
</div>
</template>

<script setup lang='ts'>
    
</script>

<style lang='scss' scoped>
.discord {
  &__wrapper {
    position: fixed;
    top: 250px;
    left: -90px;
    z-index: 100;
    writing-mode: vertical-rl;
    text-orientation: upright;
    border: none;
    transition: transform 0.5s;
    cursor: pointer;
    background: transparent;
    transform: translateX(0);
    font-family: $font-button;
    background-color: $dark-gray;
    width: auto;
    text-transform: uppercase;
    justify-content: flex-end;
    align-items: flex-end;
    padding: $spacing-l $spacing-s $spacing-l $spacing-l;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: $spacing-l;
    border-radius: 10px;
    

    &:hover {
      transform: translateX(80px);
    }

    &--text {
      margin: 0;
      color: $white;
      letter-spacing: $letter-spacing-wide  ;
    }
  }
}
</style>