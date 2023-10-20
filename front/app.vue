<template>
  <div>
    <header-ono-header />
    <NuxtPage />
  </div>
</template>

<script>

useHead(() => ({
  link: [
    { rel: 'stylesheet', href: 'https://site-assets.fontawesome.com/releases/v6.4.0/css/all.css' },
    { rel: 'stylesheet', href: 'https://site-assets.fontawesome.com/releases/v6.4.0/css/sharp-solid.css' },
    { rel: 'stylesheet', href: 'https://site-assets.fontawesome.com/releases/v6.4.0/css/sharp-regular.css' },
    { rel: 'stylesheet', href: 'https://site-assets.fontawesome.com/releases/v6.4.0/css/sharp-light.css' }
  ]
}))

import 'sanitize.css';
import 'sanitize.css/forms.css';
import 'sanitize.css/typography.css';
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Roboto:wght@400;500;700&display=swap');

body {
  // background-color: $background-color;
  background-color: $dark-main;

}
</style>