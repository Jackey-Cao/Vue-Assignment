<script setup>
import axios from "axios";
import { ref } from "vue";

const movie = ref(null);
const title = ref(null);
const runtime = ref(null);
let movieData = ref("");

const getMovie = async () => {
  movieData.value = (
    await axios.get(`https://api.themoviedb.org/3/movie/${movie.value}`, {
      params: {
        api_key: "e8016904e176c4cc2f25acfd19077f5c",
        include_adult: "false",
        append_to_response: "videos",
      },
    })
  ).data;
  console.log(movieData);
};
</script>

<template>

  <div class="movies">
    <select v-model="movie">
      <option value="671">Harry Potter and the Philosopher's Stone</option>
      <option value="672">Harry Potter and the Chamber of Secrets</option>
      <option value="673">Harry Potter and the Prisoner of Azkaban</option>
      <option value="674">Harry Potter and the Goblet of Fire</option>
      <option value="675">Harry Potter And The Order of the Phoenix</option>
      <option value="767">Harry Potter And The Half-Blood Prince</option>
      <option value="12444">Harry Potter And The Deathly Hallows: Part 1 </option>
      <option value="12445">Harry Potter And The Deathly Hallows: Part 2</option>
      <option value="361743">Top Gun: Maverick</option>
      <option value="438148">Minions: The Rise of Gru</option>
    </select>
    <button @click="getMovie">Get</button>
    <div>

    </div>
    <p>{{ movieData.title }}</p>
    <h1>{{ movieData.release_date }}</h1>
    <!-- <div v-if="weather">
      <p>Lat: {{ weather.latitude }} deg.</p>
      <p>Long: {{ weather.longitude }} deg.</p>
      <p>Temp: {{ weather.current_weather.temperature }} C</p>
      <p>Windspeed: {{ weather.current_weather.windspeed }} km/h</p>
      <p>Wind Direction: {{ weather.current_weather.winddirection }} deg.</p>
    </div> -->
  </div>

</template>

<style scoped>

</style>
