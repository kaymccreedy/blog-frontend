<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Blog",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("posts").then((response) => {
        this.posts = response.data;
        console.log("All Posts: ", this.posts);
      });
    },
  },
};
</script>

<template>
  <div class="posts">
    <h1>{{ message }}</h1>
    <router-link to="/posts/new">Create Post</router-link>
    <p v-for="post in posts" v-bind:key="post.id">
      User: {{ post.user_id }}
      <br />
      {{ post.title }}
      <br />
      <img :src="post.image" width="500" />
      <br />
      {{ post.body }}
      <br />
      <br />
    </p>
  </div>
</template>
