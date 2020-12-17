<template>
  <div>
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="">
    <form v-on:submit.prevent="submit()">
      <h1>Create a Blog Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label> 
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="body">
        <small class="text-danger">{{ 100 - body.length }} Characters Remaining</small>
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      body: "",
      image: "",
      errors: [],
      status: ""
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image
      };
      axios
        .post("/api/posts", params)
        .then(response => {
          this.$parent.flashMessage = "Post Created Successfully!"
          this.$router.push("/postsindex");
        })
        .catch(error => {
          this.status = error.response.status;
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>