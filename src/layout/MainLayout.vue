<template>
  <main>
    <AsideMenu />
    <section>
      <HeaderLayout />
      <slot></slot>
    </section>
  </main>
</template>

<script setup lang="ts">
import HeaderLayout from './HeaderLayout.vue';
import AsideMenu from './AsideMenu.vue';
</script>

<style scoped lang="scss">
main {
  display: flex;
  width: 100vw;
  // height: 100vh;
  overflow: hidden;
}

section {
  width: 100%;
}
</style>
