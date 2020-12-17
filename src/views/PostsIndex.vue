<template>
  <div class="postsindex">
    <h1>All Posts</h1>
    <div>
      Search: <input v-model="titleFilter" type="text">
    </div>

    <div v-for="post in filterBy (posts, titleFilter, 'title')">
      <div class="card" style="width: 18rem;">
        <img v-bind:src="`${post.image}`" class="card-img-top" v-bind:alt="`${post.title}`">
        <div class="card-body">
          <router-link v-bind:to="`/posts/${post.id}`">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.body }}</p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from 'axios'
import Vue2Filters from 'vue2-filters'

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      posts: [],
      titleFilter: ""
    };
  },
  created: function() {
    axios.get('/api/posts').then(response => {
      console.log("posts index", response);
      this.posts = response.data
    });
  },
  methods: {}
};
</script>