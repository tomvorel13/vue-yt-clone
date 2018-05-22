<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
          <VideoDetail :video="selectedVideo"></VideoDetail>
          <VideoList 
            @videoSelect="onVideoSelect"
            :videos="videos"
          >
          </VideoList>
        </div>
    </div>
</template>

<script>
import SearchBar from '@/components/SearchBar'
import VideoList from '@/components/VideoList'
import VideoDetail from '@/components/VideoDetail'

import axios from 'axios'
const API_KEY = 'AIzaSyAnWXMZae0QcxP-HgkOJ3Z_ClqP5F89O-Y'

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      videos: [],
      selectedVideo: null
    }
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
        })
        .then(res => {
          this.videos = res.data.items
        })
        .catch(err => console.log(err))
    },
    onVideoSelect(video) {
      this.selectedVideo = video
    }
  }
}
</script>

<style>
</style>
