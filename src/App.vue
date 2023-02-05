<script setup>
import {ref, computed, onMounted} from 'vue'

import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([])
const favorito = ref('')
const postXpage = 10
const inicio = ref(0)
const fin = ref(postXpage)
const loading = ref(true);

const cambiarFavorito = (title) => {
  favorito.value = title
}

const previusPage = () => {
  inicio.value = inicio.value - postXpage
  fin.value = fin.value - postXpage
}

const nextPage = () => {
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
}


//onMounted(async() => {
//  try {
//    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//    posts.value = await res.json()
//  } catch (error) {
//    console.log(error)
//  } finally {
//    loading.value = false
//  }
//})

//fetch('https://jsonplaceholder.typicode.com/posts')
//  .then(res => res.json())
//  .then(data => posts.value = data)
//  .finally(() => loading.value = false)

const preFetch = async() => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    loading.value = false
  }
}

preFetch();

const maxLength = computed(() => posts.value.length )

</script>
<template>
  <LoadingSpinner v-if="loading" />
  <div v-else class="container">
    <h1>App</h1>
    <h2>Mi Post Favorito: {{ favorito }}</h2>
    <PaginatePost class="mb-2" :inicio="inicio" :fin="fin" :totalSize="maxLength" @nextPage = "nextPage" @previusPage = "previusPage"></PaginatePost>
    <BlogPost
      v-for="(post, index) in posts.slice(inicio, fin)"  
      :key="index"
      :id = "post.id"
      :title="post.title"
      :content="post.body"
      colorText="primary"
      @cambiarFavorito="cambiarFavorito"
      class="mb-2"
    ></BlogPost>
  </div>
</template>