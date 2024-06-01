<script setup lang="ts">
import { ref } from 'vue'
import http from '@/plugins/axios'
import router from '@/router'

const props = defineProps<{
  ENDPOINT_API: string
}>()

const ENDPOINT = props.ENDPOINT_API ?? ''
const titulo = ref('')
const sinopsis = ref('')

async function crearSeries() {
  await http
    .post(ENDPOINT, { titulo: titulo.value, sinopsis: sinopsis.value })
    .then(() => router.push('/series'))
}

function goBack() {
  router.go(-1)
}
</script>

<template>
  <div class="container">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><RouterLink to="/">Inicio</RouterLink></li>
        <li class="breadcrumb-item">
          <RouterLink to="/series">Series</RouterLink>
        </li>
        <li class="breadcrumb-item active" aria-current="page">Crear</li>
      </ol>
    </nav>

    <div class="row">
      <h2>Crear Nueva serie</h2>
    </div>

    <div class="row">
      <form @submit.prevent="crearSeries">
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="titulo" placeholder="titulo" required />
          <label for="titulo">Titulo</label>
        </div>
        <div class="form-floating">
          <input
            type="text"
            class="form-control"
            v-model="sinopsis"
            placeholder="sinopsis"
            required
          />
          <label for="sinopsis">sinopsis</label>
        </div>
        <div class="text-center mt-3">
          <button type="submit" class="btn btn-primary btn-lg">
            <font-awesome-icon icon="fa-solid fa-save" /> Crear
          </button>
        </div>
      </form>
    </div>
    <div class="text-left">
      <button class="btn btn-link" @click="goBack">Volver</button>
    </div>
  </div>
</template>

<style></style>
