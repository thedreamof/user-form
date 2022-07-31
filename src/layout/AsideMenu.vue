<template>
  <aside class="aside">
    <section class="logo">
      <img class="img" src="@/assets/LogoAma.png" alt="Logo" />
    </section>

    <section class="menu">
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
    </section>

    <section class="options">
      <div class="item"></div>
    </section>
  </aside>
</template>

<script setup lang="ts"></script>

<style scoped lang="scss">
.aside {
  width: 100px;
}

.logo {
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;

  img {
    height: 50px;
    border-right: 1px solid var(--background-3);
  }
}

.menu {
  height: calc(100vh - 160px);
  background: var(--background-6);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.item {
  display: block;
  height: 50px;
  width: 50px;
  background: var(--background-5);
  border-radius: 50%;
  margin: 10px;
}

.options {
  height: 80px;
  background: var(--background-7);
  display: flex;
  justify-content: center;
  align-items: center;

  .item {
    margin: 0;
  }
}
</style>
