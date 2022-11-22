<script setup>
import axios from "axios";
import { ref } from "vue";


const movie = ref(null);
const  = async () => {

      },
</script>

<template>

<div class="movies">
    <select v-model="movie">
      <option value="671">Harry Potter and the Philosopher's Stone</option>
      <option value="672">Harry Potter and the Chamber of Secrets</option>
      <option value="673">Harry Potter and the Prisoner of Azkaban</option>
      <option value="674">Harry Potter and the Goblet of Fire</option>
    </select>
    <button @click="selectMovie">Get</button>
    <div v-if="weather">
      <p>Lat: {{ weather.latitude }} deg.</p>
      <p>Long: {{ weather.longitude }} deg.</p>
      <p>Temp: {{ weather.current_weather.temperature }} C</p>
      <p>Windspeed: {{ weather.current_weather.windspeed }} km/h</p>
      <p>Wind Direction: {{ weather.current_weather.winddirection }} deg.</p>
    </div>
  </div>
  function movie_selector() {
  for (let i = 0; i < 10; i++) {
    if (document.getElementById("movies").selectedIndex == i) {
      return document.getElementById("movies").value
    }
  }
};

button.addEventListener('click', async () => {
  let response = axios.get("https://api.themoviedb.org/3/search/movie", {
    params: {
      api_key: "e8016904e176c4cc2f25acfd19077f5c",
      include_adult: "false",
      query: movie_selector(),
    }
  });
  response = response.then((moviesData) => {
    for (let movie of moviesData.data.results) {
      axios.get(`https://api.themoviedb.org/3/movie/${movie.id}`, {
        params: {
          api_key: "e8016904e176c4cc2f25acfd19077f5c",
          append_to_response: "videos",
        }
      }).then((movieData) => {

        let option = movieData.data

        const screen = document.getElementById('screen');
        screen.removeAttribute('hidden')

        title = document.getElementById("title");
        title.innerHTML = `${option.title}`;
        runtime = document.getElementById("runtime");
        runtime.innerHTML = `Run Time (Mins): ${option.runtime}`;
        language = document.getElementById("language");
        language.innerHTML = `Language: ${option.original_language}`;
        releasedate = document.getElementById("releasedate");
        releasedate.innerHTML = `Released Date: ${option.release_date}`;
        popularity = document.getElementById("popularity");
        popularity.innerHTML = `Popularity: ${option.popularity}`;
        revenue = document.getElementById("revenue");
        revenue.innerHTML = `Revenue: $${option.revenue}`;
        avgvote = document.getElementById("avgvote");
        avgvote.innerHTML = `Average Vote: ${option.vote_average}`;
        votecount = document.getElementById("votecount");
        votecount.innerHTML = `Vote Count: ${option.vote_count}`;
        overview = document.getElementById("overview");
        overview.innerHTML = `${option.overview}`;

        const trailers = option.videos.results.filter((trailer) => trailer.type === "Trailer");
        video.src = `https://www.youtube.com/embed/${trailers.at(0).key}`
        cover.src = `https://image.tmdb.org/t/p/w500${movie.poster_path}`;
      });
    }
  });
});
</template>

<style scoped>
</style>
