<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.editPostParams = response.data;
        console.log("Post", this.post);
      });
    },
    editPost: function () {
      axios
        .patch("/posts/" + this.$route.params.id, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          localStorage.setItem("flashMessage", "Post Updated");
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="editPost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="editPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
