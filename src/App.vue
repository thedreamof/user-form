<template>
  <MainLayout>
    <TestView />
  </MainLayout>
</template>

<script setup lang="ts">
import MainLayout from './layout/MainLayout.vue';
import TestView from './views/TestView.vue';
</script>

<style lang="scss">
.button {
  display: block;
  background: var(--basic);
  padding: 10px 20px;
  margin: 5px;
  border-radius: 20px;
  cursor: pointer;
  border: none;
  white-space: nowrap;

  &:hover {
    // background: darken(var(--basic), 1);
    background: lightgray;
  }

  &.is-primary {
    background: var(--primary);
    color: white;

    &:hover {
      // background: darken(var(--basic), 1);
      background: lightblue;
    }
  }

  &.is-secondary {
    background: var(--secondary);
    color: white;
    &:hover {
      // background: darken(var(--basic), 1);
      background: tomato;
    }
  }

  &.is-disabled {
    background-color: var(--background-3);
    color: var(--text-light);
    cursor: not-allowed;

    &:hover {
      background: lightgray;
    }
  }
}
</style>
