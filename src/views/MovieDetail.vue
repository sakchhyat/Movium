<template>
  <div class="container">
      <div class="feature-card">
        <img :src="movie.Poster" alt="Movie Poster" class="feature-img" />
      </div>
      <div class="detail">
        <h1>{{ movie.Title }}</h1>
        <h3>{{ movie.Year }}</h3>
        <p>{{ movie.Plot }}</p>
      </div>
    </div>
</template>

<script>

import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '@/env.js'

export default {
  setup () {
    const movie = ref({})
    const route = useRoute()

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data
        })
    })

    return {
      movie,
      route,
      onBeforeMount
    }
  }
}
</script>

<style lang="scss">
.container{
    width: 100%;
    margin: 0 auto;
    padding: 30px;
  .feature-card {
    width: 20%;
    float: right;
    position: relative;
    // background-color: #fff;

    .feature-img {
      display: block;
      // width: 50%;
      // padding: 0 0%;
      height: 400px;
      // margin: 0 auto;
      // align-items: center;
      // justify-content: center;
      // object-fit: cover;
      // position: relative;
      z-index: 0;
    }
  }
  .detail {
      width: 80%;
      float: left;
      min-height: 400px;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
    }
    h1 {
      text-align: center;
      color: #FFF;
      margin-bottom: 16px;
    }
    h3 {
      text-align: center;
      color: #FFF;
      margin-bottom: 16px;
    }
    p {
      color: #FFF;
    }
}
</style>
