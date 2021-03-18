<template>
  <div class="container">
    <nav class="navbar navbar-light bg-light">
      <span class="navbar-brand mb-0 h1">Navbar</span>
    </nav>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
      <VideoDetail :video="selectedVideo"></VideoDetail>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';
const API_KEY = 'AIzaSyA-MMV9RYdJGDgy85YQC0LMlyXhCFWmyLU';
export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data: function() {
    return {
      videos: [],
      selectedVideo: null,
    };
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm,
          },
        })
        .then((res) => (this.videos = res.data.items));
    },
    onVideoSelect(video) {
      console.log(video);
      this.selectedVideo = video;
    },
  },
};
</script>

<style scoped></style>
