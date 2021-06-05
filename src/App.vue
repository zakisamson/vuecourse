<template>
  <div id="app">
    <search-bar @termChange="onTermChange" />
    <video-list :videos="videos_state"></video-list>
    {{ videos.length }}
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
const API_KEY = "AIzaSyCc6Qxhwcp6tacnWImV2tq72VJugz-mgx4";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((response) => {
          this.videos_state = response.data.items;
        });
    },
  },
  data() {
    return {
      videos_state: [],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
