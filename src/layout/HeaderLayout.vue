<template>
  <header class="header">
    <div class="info-page">
      <div class="logo"></div>
      <div class="info">
        <div class="subtitle">Sodexo suite</div>
        <div class="title">Administración de Beneficiario</div>
      </div>
    </div>

    <div class="user">
      <div class="logo"></div>
      <div class="options"></div>
    </div>
  </header>
</template>

<script setup lang="ts"></script>

<style scoped lang="scss">
.header {
  height: 80px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.logo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
  background: var(--background-3);
}

.info-page {
  display: flex;
  align-items: center;
  width: 100%;
  margin-left: 15px;
}

.subtitle {
  color: var(--text-light);
}

.title {
  font-weight: bold;
}

.user {
  width: 300px;
  display: flex;
  align-items: center;
}
.options {
  height: 50px;
  width: 200px;
  background: var(--background-3);
  border-radius: 25px;
  margin-right: 15px;
}
</style>
