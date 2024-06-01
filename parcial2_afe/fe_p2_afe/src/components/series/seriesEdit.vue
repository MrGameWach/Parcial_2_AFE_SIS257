<script setup lang="ts">
import { onMounted, ref } from 'vue'
import http from '@/plugins/axios'
import router from '@/router'

const props = defineProps<{
  ENDPOINT_API: string
}>()

const ENDPOINT = props.ENDPOINT_API ?? ''
const titulo = ref('')
const sinopsis = ref('')
const id = router.currentRoute.value.params['id']

async function editarSeries() {
  await http
    .patch(`${ENDPOINT}/${id}`, {
      titulo: titulo.value,
      sinopsis: sinopsis.value
    })
    .then(() => router.push('/series'))
}

async function getSeries() {
  await http.get(`${ENDPOINT}/${id}`).then((response) => {
    ;(titulo.value = response.data.titulo), (sinopsis.value = response.data.sinopsis)
  })
}

function goBack() {
  router.go(-1)
}

onMounted(() => {
  getSeries()
})
</script>

<template>
  <div class="container">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><RouterLink to="/">Inicio</RouterLink></li>
        <li class="breadcrumb-item">
          <RouterLink to="/series">Intérpretes</RouterLink>
        </li>
        <li class="breadcrumb-item active" aria-current="page">Editar</li>
      </ol>
    </nav>

    <div class="row">
      <h2>Editar Intérprete</h2>
    </div>

    <div class="row">
      <form @submit.prevent="editarSeries">
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="titulo" placeholder="titulo" required />
          <label for="titulo">titulo</label>
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
            <font-awesome-icon icon="fa-solid fa-save" /> Guardar
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
