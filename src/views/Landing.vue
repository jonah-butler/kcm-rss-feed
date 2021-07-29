<template>
  <v-app id="inspire">
    <TopNav />
    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <SideNav
          :feed="feeds"/>
          <MainContent />
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
      // feed: {
      //   title: '',
      //   url: '',
      //   imageUrl: '',
      //   posts: null,
      // },
      // currentPost: null,
      test: 'what up',
      feeds: Feeds.feeds,
    };
  },
  methods: {
    printPosts(value) {
      // eslint-disable-next-line
      console.log(value);
    },
    async getPosts() {
      // let blogs = await fetch('https://www.simplifyingthemarket.com/en/feed/?a=186161-a1b0b6b3364ed92fe215bff8a46af47a%2F');
      // blogs = await blogs.text();
      // blogs = new window.DOMParser().parseFromString(blogs, 'text/xml');
      // // eslint-disable-next-line
      //  this.feed.posts = blogs.getElementsByTagName('item');

      // eslint-disable-next-line
      // console.log(blogs);
      // eslint-disable-next-line
      // console.log(blogs.getElementByTagName('link'));
    },
  },
};
</script>

<style>
  /* .v-list{
    height: 100vh;
  } */

</style>
