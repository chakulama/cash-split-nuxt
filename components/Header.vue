<template>
  <div class="header">
    <div class="header__logo">LOGO</div>
    <h1 class="header__description">Calculate who pays whom how much</h1>
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped lang="scss">
.header {
  @apply text-white bg-green-700 w-full h-28 flex flex-col items-center rounded-b-3xl;
  &__logo {
    @apply text-white;
  }
  &__description {
    @apply text-2xl;
  }
}
</style>
