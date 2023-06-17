<template>
  <div class="post_form">
    <h5>New Post</h5>
    <input type="text" ref="username_input" placeholder="Username" />
    <input type="text" ref="image_input" placeholder="Image URL" />
    <textarea
      ref="content_input"
      placeholder="Content"
      cols="30"
      rows="10"
    ></textarea>
    <button @click="new_post">SUBMIT</button>
    <h5>{{ status }}</h5>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      status: undefined,
    };
  },
  methods: {
    new_post() {
      this.status = "Adding Post";
      axios
        .request({
          url: `${process.env.VUE_APP_BASE_URL}/api/post`,
          method: "POST",
          data: {
            username: this.$refs["username_input"].value,
            image_url: this.$refs["image_input"].value,
            content: this.$refs["content_input"].value,
          },
        })
        .then((response) => {
          response;
          this.status = "Post Added!";
          this.$root.$emit('new_post');
        })
        .catch((error) => {
          error;
          this.status = "Something has gone wrong. Sorry."
        });
    },
  },
};
</script>

<style scoped>

.post_form {
    display: grid;
    max-width: 500px;
    place-items: center;
}
</style>