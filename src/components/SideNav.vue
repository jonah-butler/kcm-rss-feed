<template>
  <v-col cols="2">
    <v-sheet rounded="lg">
      <v-list color="transparent">
        <v-list-item
        >
          <v-list-item-content>
            <v-list-item-title class="text-wrap">
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-sheet>
  </v-col>
</template>

<script>

export default {
  mounted() {
    // eslint-disable-next-line
    // console.log(this.feeds);
  },
  data() {
    return {
      feeds: this.feed,
    };
  },
  methods: {
    async fetchPosts(url) {
      let blogs = await fetch(url);
      blogs = await blogs.text();
      blogs = new window.DOMParser().parseFromString(blogs, 'text/xml');
      this.$emit('posts', blogs);
    },
  },
  props: {
    feed: {
      type: Array,
    },
  },
};
</script>

<style scoped>

</style>
