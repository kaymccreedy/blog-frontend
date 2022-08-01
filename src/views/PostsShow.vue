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
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.post = response.data;
        console.log("Post", this.post);
      });
    },
    destroyPost: function () {
      axios.delete("/posts/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.$router.push("/posts");
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
    |
    <router-link :to="`/posts/${post.id}/edit`">Edit Post</router-link>
    <br />
    <div class="link" v-on:click="destroyPost">Delete Post</div>
  </div>
</template>
