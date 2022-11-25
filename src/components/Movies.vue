<script setup>
import axios from "axios";
import { ref } from "vue";

const movie = ref(null);
const movieData = ref(null);

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
};
</script>

<template>
  <body>
    <label id="label" for="movies">Choose a Movie:</label>
    <div>
      <select id="movies" v-model="movie">
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
      <button id="button" @click="getMovie">Get</button>

      <div class="display" v-if="movieData">
        <h1 id="title">{{ movieData.title }}</h1>
        <iframe id="video" :src="`https://www.youtube.com/embed/${movieData.videos.results.filter((trailer) => trailer.type === 'Trailer').at(0).key}`" frameborder="0"></iframe>
        <p id="runTime">Runtime: {{ movieData.runtime }} Mins</p>
        <p id="language">Language: {{ movieData.original_language }}</p>
        <p id="releaseDate">Release Date: {{ movieData.release_date }}</p>
        <p id="overview">{{ movieData.overview }}</p>
        <p id="popularity">Popularity: {{ movieData.popularity }}</p>
        <p id="avgVote">Average Vote: {{ movieData.vote_average }}</p>
        <p id="voteCount">Vote Count: {{ movieData.vote_count }}</p>
        <p id="revenue">Revenue: ${{ movieData.revenue }}</p>
        <img id="cover" :src="`https://image.tmdb.org/t/p/w500${movieData.poster_path}`" alt="">
      </div>
    </div>
  </body>
</template>

<style scoped>
body {
  background-color: rgba(49, 4, 4, 0.763);
  height: 200vh;
}

#label {
  position: absolute;
  color: white;
  padding-top: 0.5vw;
  padding-left: 31vw;
  font-weight: bold;
  font-family: Verdana, Tahoma, sans-serif;
  font-size: 1vw;
}

#movies {
  color: black;
  margin-left: 41vw;
  margin-top: 0.5vw;
  background-color: aquamarine;
  border-color: black;
  font-weight: bold;
  font-family: Verdana, Tahoma, sans-serif;
  font-size: 1vw;
  text-align: center;
}

#button {
  font-size: 1.5vw;
  margin-top: 2vw;
  color: rgb(0, 0, 0);
  background-color: aquamarine;
  border-color: black;
  font-weight: bold;
  border-width: 2px;
  margin-left: 46.5vw;
  cursor: pointer;
}

#title {
  font-size: 3.5vw;
  margin-top: 3vw;
  color:aquamarine;
  text-align: center;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bolder;
}

#video {
  display: block;
  margin-left: auto;
  margin-right: auto;
  height: 27vw;
  aspect-ratio: 16 / 9;
  border-width: 2px;
  border-color: aquamarine;
}

#cover {
  margin-top: 6vw;
  margin-left: 7vw;
  height: 25vw;
  aspect-ratio: 2 / 3;
}

#runTime {
  position: absolute;
  font-size: 1.5vw;
  margin-top: 10vw;
  margin-left: 28vw;
  color: white;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#language {
  position: absolute;
  font-size: 1.5vw;
  margin-top: 10vw;
  margin-left: 50vw;
  color: white;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-transform: capitalize;
}

#releaseDate {
  position: absolute;
  font-size: 1.5vw;
  margin-top: 10vw;
  margin-left: 70vw;
  color: white;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#overview {
  position: absolute;
  text-align: center;
  font-size: 1.2vw;
  margin-top: 17vw;
  margin-left: 25vw;
  margin-right: 8vw;
  color: white;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#popularity {
  position: absolute;
  font-size: 1.5vw;
  margin-left: 28vw;
  margin-top: 35vw;
  color: aquamarine;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#avgVote {
  position: absolute;
  font-size: 1.5vw;
  margin-left: 51vw;
  margin-top: 35vw;
  color: aquamarine;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#voteCount {
  position: absolute;
  font-size: 1.5vw;
  margin-left: 75vw;
  margin-top: 35vw;
  color: aquamarine;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#revenue {
  position: absolute;
  font-size: 1.5vw;
  margin-left: 50vw;
  margin-top: 43vw;
  color: aquamarine;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
