<template>
  <div class="container">
    <a href="#" :style="styleObject">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      {{ textButton }}
    </a>
  </div>
</template>

<script setup lang='ts'>
import { defineProps, computed } from 'vue';

const { textButton, color } = defineProps({
  textButton : {
    type : String,
    default : 'Button'
  },
  color: {
    type: String,
    default: 'FF0000'
  }
});

const styleObject = computed(() => {
  const colorValue = color.startsWith('#') ? color : `#${color}`;
  return {
    '--clr': colorValue
  };
});

</script>

<style lang='scss' scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 120px;

    a {
      position: relative;
      padding: 16px 30px;
      font-size: 1.5em;
      color: var(--clr);
      text-shadow: 0 0 15px var(--clr);
      text-decoration: none;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      transition: 0.5s;
      border: 2px solid rgba(0,0,0,0.5);

      span {
        position: absolute;
        background: var(--clr);
        pointer-events: none;
        box-shadow: 
          0 0 10px var(--clr),
          0 0 20px var(--clr),
          0 0 30px var(--clr),
          0 0 50px var(--clr),
          0 0 100px var(--clr);

        &:nth-child(1), &:nth-child(3) {    
          width: 40px;
          height: 4px;
        }

        &:nth-child(2), &:nth-child(4) {    
          width: 4px;
          height: 40px;
        }

        &:nth-child(1) {
          top: calc(50% - 2px);
          left: -50px;
          transform-origin: left;
          transition: 0.5s ease-in-out;
          transition-delay: 0.25s;
        }

        &:nth-child(2) {
          left: calc(50% - 2px);
          top: -50px;
          transform-origin: top;
          transition: 0.5s ease-in-out;
          transition-delay: 0.25s;
        }

        &:nth-child(3) {
          top: calc(50% - 2px);
          right: -50px;
          transform-origin: right;
          transition: 0.5s ease-in-out;
          transition-delay: 0.25s;
        }

        &:nth-child(4) {
          left: calc(50% - 2px);
          bottom: -50px;
          transform-origin: bottom;
          transition: 0.5s ease-in-out;
          transition-delay: 0.25s;
        }
      }

      &:hover {
        color: $white;
        border: 2px solid rgba(0,0,0,0);
        text-shadow: 0 0 0px var(--clr);

        &::before{
        transform: scale(1);
        transition-delay: 0.5s;
        box-shadow: 
          0 0 10px var(--clr),
          0 0 30px var(--clr),
          0 0 60px var(--clr);
        }

        span:nth-child(1) {
          left: 50%;
          transform: scaleX(0);
          transition-delay: 0s;
        }

        span:nth-child(2) {
          top: 50%;
          transform: scaleY(0);
          transition-delay: 0s;
        }

        span:nth-child(3) {
          right: 50%;
          transform: scaleX(0);
          transition-delay: 0s;
        }

        span:nth-child(4) {
          bottom: 50%;
          transform: scaleY(0);
          transition-delay: 0s;
        }
      }

      &::before{
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: var(--clr);
        z-index: -1;
        transform: scale(0);
        transition: 0.5s;
      }
    }
  }
</style>