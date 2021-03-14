<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
const API_KEY = 'AIzaSyA-MMV9RYdJGDgy85YQC0LMlyXhCFWmyLU';
export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
  },
  data: function() {
    return { videos: [] };
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
    },
  },
};
</script>
