<template>
  <div >
    <Episode v-for="(episode, index) in episodes" :key="index" :episode="episode" />
  </div>
</template>

<script>
import Episode from "./Episode.vue"
export default {
  name: 'EpisodeList',
  props: {
    episodes: {
      type: Array,
      required: true,
    },
  },
  components: {
    Episode,
  },
}
</script>