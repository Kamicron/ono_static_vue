<template>
  <div class="presentaion">
    <div class="presentation__block">
      <border-text 
        blur text="Old not Obsolete" 
        :fontSize="24" 
        :borderWidth="4" color="white"
      />
    </div>
    <div class="presentation__block">
      <border-text 
        blur text="Old not Obsolete" 
        :fontSize="24" 
        :borderWidth="4" color="white"
      />
    </div>
  </div>
</template>

<script setup lang='ts'>

</script>

<style lang='scss' scoped>
.presentaion {
  padding-top: 150px;
  display: flex;
  max-width: 1220px;
  margin: auto;
  justify-content: center;

  &__block {}
}
</style>