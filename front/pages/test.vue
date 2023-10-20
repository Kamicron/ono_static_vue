<template>
  <div class="test">
    <button-v-2 text-button="Voir plus" :color="color"/>  
    <button-v-2 text-button="Voir plus" color="#00FF00"/>  
  </div>
</template>

<script setup lang="ts">
import { colors } from '@/assets/js/variables/colors';
import { ref } from 'vue';  
const color = ref(colors.alternative);
</script>

<style scoped lang="scss">
.test {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 500px;
}
</style>