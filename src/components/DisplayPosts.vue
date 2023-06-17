<template>
  <div>
    <h3>POSTS</h3>
    <h4>{{ status }}</h4>
    <section class="posts_container">
      <article v-for="(post, i) in posts" :key="i" class="post">
        <img :src="post['image_url']" alt="The image for the post" />
        <p>{{ post["content"] }}</p>
        <h5>{{ post["username"] }}</h5>
      </article>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      posts: [],
      status: undefined,
    };
  },

  methods: {
    get_posts() {
      axios
        .request({
          url: `${process.env.VUE_APP_BASE_URL}/api/post`,
        })
        .then((response) => {
          this.posts = response["data"];
          if (this.posts.length === 0) this.status = "No posts! Go make some.";
        })
        .catch((error) => {
          console.log(error);
          this.status =
            "Sorry, something has gone wrong. Please refresh later.";
        });
    },
  },

  mounted() {
    this.get_posts();
    this.$root.$on(`new_post`, this.get_posts);
  },
};
</script>

<style scoped>

.posts_container {
    display: grid;
    place-items: center;
    width: 100%;
    gap: 30px;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

.post{ 
    display: grid;
    place-items: center;
    text-align: center;
    gap: 15px;
    padding: 10px;
}
</style>