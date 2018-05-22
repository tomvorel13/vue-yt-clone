<template>
    <ul class="list-group col-md-4">
        <VideoListItem 
            @videoSelect="onVideoSelect"
            v-for="(video, index) in videos" 
            :key="index" 
            :video="video"
        />
    </ul>    
</template>

<script>
import VideoListItem from '@/components/VideoListItem'

export default {
  name: 'VideoList',
  components: {
    VideoListItem
  },
  props: {
    videos: Array
  },
  methods: {
    onVideoSelect(video) {
      this.$emit('videoSelect', video)
    }
  }
}
</script>

<style>
</style>
