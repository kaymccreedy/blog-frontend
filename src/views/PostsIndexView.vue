<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function () {
    return {
      message: "Blog",
      posts: [],
      users: [],
      currentPost: [],
      titleFilter: "",
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
    indexUsers: function () {
      axios.get("users").then((response) => {
        this.users = response.data;
        console.log("All Users: ", this.users);
      });
    },
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
    filterPosts: function () {
      return this.posts.filter((post) => {
        var lowerTitle = post.title.toLowerCase();
        var lowerTitleFilter = this.titleFilter.toLowerCase();
        return lowerTitle.includes(lowerTitleFilter);
      });
    },
  },
};
</script>

<template>
  <div class="posts">
    <h1>{{ message }}</h1>
    <br />
    <input v-model="titleFilter" />
    &nbsp;|&nbsp;
    <router-link to="/posts/new">Create Post</router-link>
    <br />
    <p
      v-for="post in filterPosts()"
      v-bind:key="post.id"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
    >
      <br />
      User: {{ post.user_id }}
      <br />
      <router-link :to="`/posts/${post.id}`">
        {{ post.title }}
      </router-link>
      <br />
      {{ post.body }}
      <br />
      <small>
        <em>Updated: {{ relativeDate(post.updated_at) }}</em>
      </small>
      <br />
      <br />
    </p>
  </div>
</template>

<style>
.selected {
  background-color: #fcfbf7;
}
</style>
