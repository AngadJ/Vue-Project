<script setup>
import { ref } from "vue";
import axios from "axios";
 
const id = ref("");
const movie = ref(null);
 
const getMovies = async () => {
  const data = id.value;
  movie.value = (
    await axios.get(`https://api.themoviedb.org/3/movie/${data}`, {
      params: {
        api_key: "f944b70daa59b60504fca0c383e63483",
        append_to_response: "videos",

      },
    })
  ).data;
};
</script>

<template>

    <h2> Wondering what movie to watch next? Select your choice of film then press the button to get some cool info on the movie.</h2>
    <label for="mainselect">Movie Options:</label>
<select v-model="id">
    <option value="480530"> Creed II</option>
    <option value="37724"> Skyfall</option>
    <option value="634649"> Spider-Man: No Way Home</option>
    <option value="161">Ocean's Eleven</option>
    <option value="299536">Avengers: Infinity War</option>
    <option value="150607">Star Wars: The Force Awakens</option>
    <option value="91314">Transformers: Age of Extinction</option>
    <option value="302699">Central Intelligence</option>
    <option value="705861"> Hustle</option>
    <option value="323675">Ride Along 2</option>
  </select>
  <button @click="getMovies">Get</button>
  <div v-if="movie" class="movie-container">

    <h1> {{movie.original_title}}</h1>
    <p> Release Date: {{movie.release_date}}</p>
    <p> Rating: {{movie.vote_average}} Stars </p>
    <p> Length of Film: {{movie.runtime}} minutes </p>
    <p> Popularity: {{movie.popularity}}</p>
    <p> Box Office: {{movie.revenue}} USD </p>
    <p> Budget: {{movie.budget}} USD </p>
    <p> Vote Count: {{movie.vote_count}} people </p>
    <p> Overview: {{movie.overview}}</p>
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="">
    <iframe :src="`https://www.youtube.com/embed/${movie.videos.results.filter((video) => video.type === 'Trailer').at(0).key}`"></iframe>

  </div>

</template>
 
<style>
body {
    background-color: slategray;
    color: black;
  
  }
  
  h1 {
    color: black;
    font-family: 'Play', sans-serif;
    font-size: 30px;
    border-color: black;
    border-width: 10px;
    border-style: double;
    padding: 15px;
    width: 250px;
    
  }
  
  h2{
    color: black;
    font-family: 'Play', sans-serif;
    border-color: black;
    border-width: 10px;
    border-style: double;
    padding: 10px;
  
  }
  
  img {
    width: 450x;
    height: 520px;
  }
  
  p {
    color: white;
    font-size: 20px;
    font-weight: bold;
  
  }
  
  iframe {
    aspect-ratio: 16 / 9;
    height: 520px;
    border-style: solid;
  
  }
  
  :hover {
  border-width: 10px;
  border-color: white;
  color: black;
  
  }
  
  label {
    font-size: 17px;
    font-family: 'Play', sans-serif;
    background-color: white;
    border-width: 10px;
    padding: 10px;
  
  }
  
  select{
    font-size: 17px;
    font-family: 'Play', sans-serif;
    background-color: white;
  
  }

  button {
    background-color: white;
    padding: 5px;
    font-family: 'Play', sans-serif;

  }

</style>