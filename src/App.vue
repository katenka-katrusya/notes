<script setup>
import AppHeader from '@/components/Header.vue';
import AppFooter from '@/components/Footer.vue';
</script>

<template>
  <div class="wrapper">
    <AppHeader />
    <div class="wrapper-content">
      <div class="container">
        <div class="view-sm isCenter">
          <RouterView />
        </div>
      </div>
    </div>
    <AppFooter />
  </div>
</template>

<style scoped lang="scss">
</style>
