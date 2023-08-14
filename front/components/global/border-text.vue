<template>
  <section class="borderText">
    <div class="borderText__container">
      <div class="borderText__item">
        <div
          :class="[dynamicClass, isHovering ? hoverClass : '']"
          :style="contentStyle"
          class="borderText__content"
          @mouseover="isHovering = true"
          @mouseleave="isHovering = false"
        >
        <slot></slot>
          {{ text }}
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const props = defineProps({
  text: String,
  fontSize: {
    type: [Number, String],
    default: 16,
  },
  borderWidth: {
    type: [Number, String],
    default: 2,
  },
  color: {
    type: String,
    default: 'white',
  },
  hoverColor: String,
});

const dynamicClass = computed(() => `--${props.color}`);
const hoverClass = computed(() => props.hoverColor ? `--${props.hoverColor}` : '');
const isHovering = ref(false);

const contentStyle = computed(() => ({
  fontSize: `${props.fontSize}px`,
  borderWidth: `${props.borderWidth}px`,
}));
</script>


<style scoped lang="scss">
$colors: (
  black: $black,
  dark-gray: $dark-gray,
  medium-gray: $medium-gray,
  light-gray: $light-gray,
  background-color: $background-color,
  white: $white,
  main-color: $main-color,
  secondary-color: $secondary-color,
);

.borderText {
  transform: skew(-45deg); // Apply the inverse skew so the text remains straight

  &__container {
    padding: 0 200px;
    display: flex;
    gap: $spacing-m;
    padding: 0;
    justify-content: center;
    align-items: center;
    margin: 0;
  }

  &__item {
    overflow: hidden;
    position: relative;
    margin-right: 10px;
    display: flex;
    align-items: center;
  }

  &__content {
    padding: 0 $spacing-l;

    transform: skew(45deg); // Apply skew to the content to create the parallelogram
    transition: border 0.3s ease-in-out, color 0.3s ease-in-out;
    color: var(--color);
    text-decoration: none;
    font-family: $font-button;
    font-size: $font-size-xl;
    letter-spacing: $letter-spacing-wide;
    font-weight: $font-weight-bold;
    border: 2px solid currentColor;

    &.--black {
      color: $black;
      border-color: $black;;
    }

    &.--dark-gray {
      color: $dark-gray;
      border-color: $dark-gray;
    }

    &.--medium-gray {
      color: $medium-gray;
      border-color: $medium-gray;
    }

    &.--light-gray {
      color: $light-gray;
      border-color: $light-gray;
    }

    &.--background-color {
      color: $background-color;
      border-color: $background-color;
    }

    &.--white {
      color: $white;
      border-color: $white;
    }

    &.--main-color {
      color: $main-color;
      border-color: $main-color;
    }

    &.--secondary-color {
      color: $secondary-color;
      border-color: $secondary-color;
    }

    &:hover {
    &.--black { border-color: $black; }
    &.--dark-gray { border-color: $dark-gray; }
    &.--medium-gray { border-color: $medium-gray; }
    &.--light-gray { border-color: $light-gray; }
    &.--background-color { border-color: $background-color; }
    &.--white { border-color: $white; }
    &.--main-color { border-color: $main-color; }
    &.--secondary-color { border-color: $secondary-color; }
  }
  }
}</style>
