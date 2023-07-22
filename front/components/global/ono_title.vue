<template>
  <div class="container">
    <h1 v-if="type === 'h1'" ref="titleRef">{{ title }}</h1>
    <h2 v-if="type === 'h2'" ref="titleRef">{{ title }}</h2>
    <h3 v-if="type === 'h3'" ref="titleRef">{{ title }}</h3>
    <h4 v-if="type === 'h4'" ref="titleRef">{{ title }}</h4>
    <h5 v-if="type === 'h5'" ref="titleRef">{{ title }}</h5>
    <h6 v-if="type === 'h6'" ref="titleRef">{{ title }}</h6>
    <svg ref="svgRef" class="underline" xmlns="http://www.w3.org/2000/svg">
      <path class="red-path" :d="`M0,20 L${titleWidth/2},20`" stroke-width="2" fill="none" />
      <path class="black-path" :d="`M${titleWidth/2},20 L${titleWidth},20 L${titleWidth + 20},0 L${titleWidth + 80},0`" stroke-width="2" fill="none" />
    </svg>
  </div>
  </template>

<script setup lang='ts'>
import { ref, onMounted, nextTick } from 'vue';
const props = defineProps({
  /* Require */
  type: {
    type: String,
    default: 'h1',
    required: true
  }
})
let title = ref('Ceci est notre roster');
let titleRef = ref<HTMLHeadingElement | null>(null);
let svgRef = ref<SVGSVGElement | null>(null);
let titleWidth = ref(0);

onMounted(async () => {
  await nextTick();
  if (titleRef.value && svgRef.value) {
    titleWidth.value = titleRef.value.getBoundingClientRect().width;
    svgRef.value.setAttribute('viewBox', `0 0 ${titleWidth.value + 80} 20`);
  }
});
</script>

<style lang='scss' scoped>
.decoration {
  width: 0;
  height: 0;
  border-bottom: 200px solid transparent;
  border-left: 500px solid $dark-gray;
}

.container {
  position: relative;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  display: inline-block;
  margin: 0;
}

.underline {
  position: absolute;
  bottom: -5px;
  height: 20px;
  left: 0;
}

.red-path {
  stroke: $secondary-color;
}

.black-path {
  stroke: $light-gray;
}
</style>
