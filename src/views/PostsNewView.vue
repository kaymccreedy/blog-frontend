<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { body: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <img :src="`https://http.dog/${status}.jpg`" width="500" v-if="status.length !== 0" />
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <h1>New Post</h1>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input
          type="text"
          v-model="newPostParams.body"
          maxlength="140"
          :class="{ atMax: 140 - newPostParams.body.length === 0 }"
        />
        <small>{{ 140 - newPostParams.body.length }} characters remaining</small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style>
.atMax {
  color: blue;
  background-color: red;
}
</style>
