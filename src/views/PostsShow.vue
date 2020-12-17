<template>
  <div class="show">
   <h1>{{ post.title }}</h1>
   <img v-bind:src="post.image" alt="post.title">
   <h2>{{ post.body }}</h2>
  </div>
</template>

<style>
</style>

<script>
import axios from 'axios'

export default {
  data: function() {
    return {
      post: {}
    };
  },
  created: function() {
    axios.get('/api/posts/' + this.$route.params.id).then(response => {
      this.post = response.data;
      console.log("show post", this.post)
    });
  },
  methods: {}
};
</script>