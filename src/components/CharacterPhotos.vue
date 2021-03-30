<template>
  <div style="display:inline-block">
    <Photo v-for="(post, index) in posts" :key="index" :post="post" />
  </div>
</template>

<script>
import Photo from "./Photo.vue"
export default {
  name: 'CharacterPhotos',
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  components: {
    Photo,
  },
}
</script>