<template>
  <v-col cols="2">
    <v-sheet rounded="lg">
      <v-list
      dense
      color="transparent">
        <v-list-item
        v-for="feed in feeds"
        :key="feed.title"
        @click="fetchPosts(feed.url)"
        link
        >
          <v-list-item-content>
            <v-list-item-title
            class="text-wrap">
              {{feed.title}}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-sheet>
  </v-col>
</template>

<script>

export default {
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
