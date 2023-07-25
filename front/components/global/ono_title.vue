<template>
  <div class="container">
    <h1 v-if="type === 'h1'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ title }}</h1>
    <h2 v-if="type === 'h2'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ props.title }}</h2>
    <h3 v-if="type === 'h3'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ props.title }}</h3>
    <h4 v-if="type === 'h4'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ props.title }}</h4>
    <h5 v-if="type === 'h5'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ props.title }}</h5>
    <h6 v-if="type === 'h6'" :class="(props.black ? 'black' : '') + (props.white ? ' white' : '')" ref="titleRef">{{ props.title }}</h6>
    <svg ref="svgRef" class="underline" xmlns="http://www.w3.org/2000/svg">
      <path class="red-path" :d="`M4,50 L${titleWidth*4},50`" stroke-width="7" stroke-linecap="round" />
      <line class="black-path" :x1="`${titleWidth*4+10}`" y1="50" :x2="`${titleWidth*4+200}`" y2="50" stroke="black" stroke-width="8" />
      <line class="black-path" :x1="`${titleWidth*4+198.8}`" y1="50.6" :x2="`${titleWidth*4+300}`" y2="4" stroke="black" stroke-width="8" />
      <line class="black-path" :x1="`${titleWidth*4+300}`" y1="4" :x2="`${titleWidth*4+500}`" y2="4" stroke="black" stroke-width="7" />

      <!-- <path class="black-path" :d="`M${titleWidth/2},20 L${titleWidth},20 L${titleWidth + 20},0 L${titleWidth + 80},0`" stroke-width="8" fill="none" /> -->
    </svg>

    <!-- <svg ref="svgRef" class="underline" viewBox="0 0 513 69" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path class="red-path" d="M0 20L209 65" stroke="#FF0000" stroke-width="7" stroke-linecap="round" />
      <line class="black-path" x1="214" y1="65" x2="368" y2="65" stroke="black" stroke-width="7" />
      <line class="black-path" x1="419.668" y1="2.26486" x2="365.244" y2="66.386" stroke="black" stroke-width="7" />
      <line class="black-path" x1="417" y1="3.5" x2="513" y2="3.5" stroke="black" stroke-width="7" />
    </svg> -->

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
  },
  title: {
    type: String,
    default: "Titre",
    required: true
  },
  white: {
    type: Boolean,
    default: false,
  },
  black: {
    type: Boolean,
    default: true,
  }
})
let title = ref(props.title);
let titleRef = ref<HTMLHeadingElement | null>(null);
let svgRef = ref<SVGSVGElement | null>(null);
let titleWidth = ref(0);

onMounted(async () => {
  await nextTick();
  if (titleRef.value && svgRef.value) {
    titleWidth.value = titleRef.value.getBoundingClientRect().width;
    svgRef.value.setAttribute('viewBox', `0 0 800 55`);
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
  bottom: 0px;
  height: 20px;
  left: 0;
}

.red-path {
  stroke: $secondary-color;
}

.black-path {
  stroke: $light-gray;
}

.black {
  color : $black
}

.white {
  color: $white;
}
</style>