<template>
  <div class="wrapper">
    <div class="logo">
    <img width="100%" src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_square_1-5bdc75aaebeb75dc7ae79426ddd9be3b2be1e342510f8202baf6bffa71d7f5c4.svg">
    </div>
    <h1>Movie Search</h1>
    <div class="search">
      <div class="input-group mb-3">
        <input type="text" id="search" name="search" @input="handleInput" v-model="searchValue" class="form-control"   placeholder="Enter the name of the movie" aria-label="small" aria-describedby="basic-addon2">
        <router-view />
    </div>
    </div>

    <div class="results">
          
        <div class="shadow-sm p-3 mb-5 bg-white rounded" id="section" v-for="item in searchResults" :key="item.results">
          <img v-bind:src= " posters + item.poster_path " >
          <h2>{{ item.title }}</h2>
          <p>{{ item.overview }}</p>
          <p>Popularity: {{ item.popularity }}</p>
          <p>Vote count: {{ item.vote_count }}</p>
        </div>
     <!-- <div>  
        <table>
          <tbody>
            <tr v-for="item in searchResults" :key="item.results">
              <td><img v-bind:src= " posters + item.poster_path " ></td>
              <td><h2>{{ item.title }}</h2></td>
              <td><p>{{ item.overview }}</p></td>
            </tr>
          </tbody>  
        </table>>
      </div>-->
          
        
      
    </div>

  </div>


</template>

<script>
import axios from "axios";
//import debounce from "lodash.debounce";

export default {
  name: "Search",
  data() {
    return {
      searchValue: "",
      searchResults: [],
      posters: "http://image.tmdb.org/t/p/w188_and_h282_bestv2/",
    };
  },
  methods: {
    handleInput() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=5c10c6b1fd1a3b2758abd74cc9280f0b&language=en-US&query=" +
            this.searchValue,
          "&include_adult=false"
        )
        .then((response) => {
          this.searchResults = response.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

p {
  font-family: 'Source Sans Pro', Arial, sans-serif;
  display: -webkit-box;
  max-height: 75px;
  overflow: hidden;
  text-overflow: ellipsis;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  font-size: 15px;
  line-height: 25px;
  padding-right: 1vw;
  padding-left: 1vw; 
}

h2 {

  font-family: 'Source Sans Pro', Arial, sans-serif;
  padding: 0.5vw;
}

.results {

  margin-left: 20vw;
  margin-right: 20vw;

}

#app {

  margin-top: 0px !important;

}

#section {

  margin-top: 20px;
  display: inline-block;
  align-items: center;
  border: 1px solid;
  border-color: gainsboro;
  border-radius: 5px;
  width: 100%;
  padding: 0 !important;
}

img {

  float: left;
}

.wrapper {

    flex-direction: column;
    display: flex;
    align-items: center;
    padding: 30px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.responsive {
  width: 50px;
  max-width: 400px;
  height: auto;
}

.logo {

  padding: 0.9vw;
}

#search {

  min-width: 300px;
}


@media only screen and (max-width: 680px) {
    #search { min-width: 0; }
}

</style>
