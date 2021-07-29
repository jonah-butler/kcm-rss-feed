<template>
  <div>
    Yo
  </div>
</template>

<script>
import Feeds from '@/feeds';

export default {
  async mounted() {
    await this.getPosts();
  },
  data() {
    return {
      feed: {
        title: '',
        url: '',
        imageUrl: '',
        posts: [],
      },
      currentPost: null,
    };
  },
  methods: {
    async getPosts() {
      let blogs = await fetch('https://www.simplifyingthemarket.com/en/feed/?a=186161-a1b0b6b3364ed92fe215bff8a46af47a%2F');
      blogs = await blogs.text();
      blogs = new window.DOMParser().parseFromString(blogs, 'text/xml');
      // eslint-disable-next-line
      console.log(Feeds, blogs);
    },
  },
};
</script>

<style>

</style>
