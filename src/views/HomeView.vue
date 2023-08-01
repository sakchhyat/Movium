<template>
    <div class="home">
      <form @submit.prevent="SearchMovie()" class="search-box">
        <input type="text" placeholder="Type in your movie(s)" v-model="search"/>
        <input type="submit" value="Search" />
      </form>
      <div class="container">
      <div class="feature-card">
        <router-link to="/movie/tt0409591">
          <img src="https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcSzYzZ8fnuDOmDN2dmhVFHoPwTZozfcjtlvsf3zdjzfgduLR0jy
          " alt="End game Poster" class="feature-img" />
        </router-link>
      </div>
      <div class="detail">
        <h1>Avengers: End game</h1>
        <h3>2018</h3>
        <p>After the devastating events of Avengers: Infinity War (2018), the universe is in ruins. With the help of remaining allies, the Avengers assemble once more in order to reverse Thanos' actions and restore balance to the universe.</p>
      </div>
    </div>
      <div class="movies-list">
        <div class="movie" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
            <div class="product-image">
              <img :src="movie.Poster" alt="Movie Poster" />
              <div class="type">{{ movie.Type }}</div>
            </div>
            <div class="detail">
              <p class="year">{{ movie.Year }}</p>
              <h3>{{ movie.Title }}</h3>
            </div>
          </router-link>
        </div>
      </div>
    </div>
</template>

<script>

import { ref } from 'vue'
import env from '@/env.js'

export default {

  setup () {
    const search = ref('')
    const movies = ref([])

    const SearchMovie = () => {
      if (search.value !== '') {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search
            search.value = ''
          })
      }
    }

    return {
      search,
      movies,
      SearchMovie
    }
  }

}
</script>

<style lang="scss">
.home {
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
  .search-box {
    width: 50%;
    margin: 0 auto;
    display: flex;
    // flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      padding: 10px 16px;

      &[type="text"] {
        width:70%;
        float:left;
        color: #FFF;
        background-color: #496583;
        font-size: 20px;
        border-radius: 8px 0px 0px 8px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
        &[type="submit"] {
        width:25%;
        float:right;
        border-radius: 0px 8px 8px 0px;
        background-color: #42B883;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3b8070;
        }
      }
    }
  }
}
.movies-list {
    width:100%;
    // float: right;
    display: flex;
    flex-wrap: wrap;

    .movie {
      max-width: 20%;
      flex: 1 1 50%;
      padding: 16px 8px;
      margin: 7px auto;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #AAA;
            font-size: 14px;
          }

          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
</style>
