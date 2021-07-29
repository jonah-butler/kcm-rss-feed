<template>
  <v-app id="inspire">
    <TopNav />
    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <SideNav
          v-on:posts="buildPosts"
          :feed="feeds"/>
          <MainContent
          :posts="channel"
          />
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TopNav from '@/components/TopNav.vue';
import SideNav from '@/components/SideNav.vue';
import MainContent from '@/components/MainContent.vue';
import Feeds from '@/feeds';

export default {
  components: {
    SideNav,
    MainContent,
    TopNav,
  },
  async mounted() {
    // eslint-disable-next-line
    // console.log(Feeds.feeds);
    // this.feeds = Feeds.feeds;
  },
  data() {
    return {
      feeds: Feeds.feeds,
      channel: {
        selected: false,
        imageURL: null,
        posts: null,
        title: null,
      },
    };
  },
  methods: {
    buildPosts(value) {
      this.channel.selected = !this.channel.selected;
      this.getImage(value);
      this.getTitle(value);
      this.getPosts(value);
    },
    getImage(tree) {
      this.channel.imageURL = tree.querySelector('channel image url').innerHTML;
    },
    getTitle(tree) {
      this.channel.title = tree.querySelector('channel title').innerHTML;
    },
    getPosts(tree) {
      this.channel.posts = tree.querySelectorAll('channel item');
    },
  },
};
</script>

<style>
  /* .v-list{
    height: 100vh;
  } */

</style>
