<template>
  <button class="button" @click="emit('click')">
    <span><slot></slot></span>
  </button>
</template>

<script setup>
import { ref, emit } from 'vue';
</script>

<style scoped lang="scss">
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  font-weight: 600;
  color: #fff;
  background-color: transparent;
  border: 3px solid #fff;
  padding: 15px 30px;
  text-align: center;
  text-decoration: none;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  transform: skewX(-20deg);

  span {
    position: relative;
    z-index: 1;
    mix-blend-mode: difference;
    transform: skewX(20deg);
  }

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #fff;
    transform: scaleY(0);
    transform-origin: top;
    transition: transform 0.3s ease-in-out;
    z-index: 0;
  }

  &:hover {
    cursor: pointer;
  }

  &:hover::before {
    transform: scaleY(1);
  }

  &:active {
    transform: scale(0.95);
  }

  &:focus {
    outline: none;
  }
}
</style>
