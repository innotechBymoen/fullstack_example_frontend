<template>
  <div>
    <new-post></new-post>
    <display-posts></display-posts>
  </div>
</template>

<script>
import DisplayPosts from '@/components/DisplayPosts.vue'
import NewPost from '@/components/NewPost.vue'

export default {
  name: 'HomeView',
  components: {
    NewPost,
    DisplayPosts
  }
}
</script>
