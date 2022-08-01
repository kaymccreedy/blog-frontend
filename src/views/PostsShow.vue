<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("posts/" + this.$route.params.id).then((response) => {
        this.post = response.data;
        console.log("Post", this.post);
      });
    },
  },
};
</script>

<template>
  <div class="post">
    <h4>{{ post.title }}</h4>
    <img :src="post.image" width="500" />
    <br />
    <p>{{ post.body }}</p>
    <br />
    <br />
    <router-link to="/posts">Back to Posts</router-link>
  </div>
</template>
