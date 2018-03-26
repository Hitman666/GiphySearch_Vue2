<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input name="title" v-model="searchTerm">

    <button @click="performSearch()">Search</button>

    <div>
        <img v-for="g in giphies" :key="g.id" :src="g.images.original.url">
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to GiphySearch",
      searchTerm: "cat",
      giphies: []
    };
  },
  methods: {
    performSearch: function() {
      console.log(this.searchTerm);

      var link = "http://api.giphy.com/v1/gifs/search?api_key=dc6zaTOxFJmzC&q=";
      var apiLink = link + this.searchTerm;

      axios
        .get(apiLink)
        .then(response => {
          this.giphies = response.data.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>