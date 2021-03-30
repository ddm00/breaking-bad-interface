<template>
  <section class="myDiv">
    <div class="h-96">
      <img
        class="w-full mt-2 rounded"
        :src="post.img"
        height="220"
        width="200"
      />
      <p class="mt-2 text-justify text-gray-700 line-clamp-4">
        {{ post.name }}
      </p>
      <p class="mt-2 text-justify text-gray-700 line-clamp-4">
       Nickname : {{ post.nickname }}
      </p>
    </div>
    <div>
      <p class="mt-4 font-bold text-gray-600">{{ post.byline }}</p>
      <p class="font-light text-gray-600">
        Status : {{ post.status }}
      </p>
    </div>
  </section>
</template>

<script>

export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
}
</script>
<style scoped>
.myDiv {
  border: 5px outset rgb(42, 158, 32);
  background-color: rgb(242, 255, 238);    
  text-align: center;
  float:left;
  margin:15px
}
</style>