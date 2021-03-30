<template>
  <section class="myPhoto" >
    <div class="h-96">
      <p class="mt-2 text-justify text-gray-700 line-clamp-4">
        {{ "S"+('0' + episode.season.trim()).slice(-2) + ('0' + episode.episode).slice(-2)  }}
      </p>
      <p class="mt-2 text-justify text-gray-700 line-clamp-4">
        {{episode.title}}
      </p>
    </div>
    <div>
      <p class="font-light text-gray-600">
       Air Date : {{ episode.air_date }}
      </p>
    </div>
  </section>
</template>

<script>

export default {
  props: {
    episode: {
      type: Object,
      required: true,
    },
  },
}
</script>
<style scoped>
.myPhoto{
border: 5px outset rgb(42, 158, 32);
  background-color: rgb(242, 255, 238);    
  text-align: center;
  float:left;
  margin:15px;
  width:200px;
  height: 180px;
}
</style>