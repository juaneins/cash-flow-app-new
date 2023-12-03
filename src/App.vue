<script setup>
//import HomeComponent from '@/components/HomeComponent.vue';
import SplashScreen from '@/components/SplashScreen.vue';
import { defineAsyncComponent } from 'vue';

const HomeAsyncComponent = defineAsyncComponent(() => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(import('./components/HomeComponent.vue'));
    }, 2500);
  });
});
</script>

<template>
  <Suspense>
    <template #default>
      <HomeAsyncComponent />
    </template>
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
