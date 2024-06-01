<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import { useAuthStore } from '@/stores/index'
const authStore = useAuthStore()
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld :msg="'SIS257' + (authStore.user ? ' - Hola ' + authStore.user : '')" />

      <nav>
        <RouterLink to="/">Inicio</RouterLink>
          <RouterLink to="/interpretes">Series</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style >
@import '@/assets/css/bootstrap.min.css';
@import '@/assets/css/bootstrap-icons.css';
@import '@/assets/css/templatemo-festava-live.css';

</style>
