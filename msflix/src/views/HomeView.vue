<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt5420376">
        <img
          src="@/images/riverdale.png"
          alt="Cobra Kai Poster"
          class="featured-img"
        />
        <div class="detail">
          <p>
            A pequena e tranquila cidade de Riverdale fica de cabeça para baixo
            quando é atingida pela misteriosa morte de Jason Blossom, um garoto
            popular do ensino médio e membro da família mais poderosa da cidade
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="Pesquise aqui o seu filme!"
        v-model="search"
      />
      <input type="submit" value="Pesquisar" />
    </form>
  </div>

  <div class="movie-list">
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
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };
    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>
<style lang="scss" scoped>
.home {
  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 600px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgb(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      h3 {
        color: white;
        margin-bottom: 16px;
      }
      p {
        color: white;
      }
    }
  }
  .search-box {
    display: flex;
    flex-direction: row;
    justify-content: center;
    padding: 16px;
    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        max-width: 500px;
        color: white;
        background-color: black;
        font-size: 20px;
        padding: 10px 16px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: white;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgb(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 200px;
        background-color: rgb(163, 1, 152);
        padding: 16px;
        color: white;
        font-size: 18px;
        text-transform: uppercase;
        transition: 0.1s;
        height: 50px;
        margin-left: 20px;
      }
    }
  }
  .movie-list {
    margin: 0px 8px;
    display: flex;
    margin: 0px 8px;
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
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
            background-color: rgb(163, 1, 152);
            color: white;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: #496583;
          padding: 8px 16px;
          flex: 1 1 100%;
          display: flex;
          flex-direction: row;
          .year {
            color: white;
            font-size: 14px;
            margin-right: 10px;
          }
          h3 {
            color: white;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
.movie-list {
  margin: 0px 8px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.movie {
  width: 200px;
  margin-bottom: 20px;
}
.product-image {
  position: relative;
  display: block;
}
.product-image {
  position: relative;
  display: block;
  img {
    display: block;
    width: 100%;
    height: 275px;
    object-fit: cover;
  }
}
.type {
  position: absolute;
  padding: 8px 16px;
  background-color: rgb(163, 1, 152);
  color: white;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}
.detail {
  background-color: rgb(163, 1, 152);
  padding: 8px 16px;
  flex: 1 1 100%;
  display: flex;
  flex-direction: row;
}
.year {
  color: white;
  font-size: 14px;
  margin-right: 10px;
}
h3 {
  color: white;
  font-weight: 600;
  font-size: 18px;
}
</style>
