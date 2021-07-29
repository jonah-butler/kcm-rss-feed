<template>
  <v-col id="mainContent">
    <v-sheet
    min-height="70vh"
    ref="mainContent"
    rounded="lg">
    <v-container
    v-if="postData && postData.title && !singlePost">
      <v-row dense>
        <v-col cols="12">
          <v-avatar
          class="mr-10"
          size="50"
          >
          <v-img
          :src="postData.imageURL">
          </v-img>
          </v-avatar>
          <v-card-title>
            {{postData.title}}
          </v-card-title>
          <v-card-subtitle>Latest Posts</v-card-subtitle>
          <v-card
            v-for="(post, index) in postData.posts"
            :key="index"
            color="white"
            class="mx-auto"
            max-width="644">
          <v-img
          :src="printImageURL(post)"
          height="200px"
          ></v-img>
            <v-card-title
            class="text-h6"
            style="padding-bottom: 0px;">
              {{ printTitle(post) }}
            </v-card-title>
            <v-card-title
            class="date">
              {{ printDate(post) }}
            </v-card-title>
            <v-card-actions>
            <v-spacer></v-spacer>
          </v-card-actions>
          <v-expand-transition>
          <div v-show="show">
            <v-card-text>
              {{ printSampleDescription(post) }}
            </v-card-text>
            <v-card-actions>
              <v-btn
              @click="showSinglePost(index)"
              text>
                Read More
              </v-btn>
            </v-card-actions>
          </div>
        </v-expand-transition>
      </v-card>
        </v-col>
      </v-row>
    </v-container>
    <v-container
    v-else-if="singlePost && postData">
    <v-btn
    id="backBtn"
    @click="goBack">Back</v-btn>
      <v-card
        color="white"
        class="mx-auto"
        max-width="644">
      <v-img
      :src="printImageURL(singlePost)"
      height="200px"
      ></v-img>
      <v-card-title
      class="text-h6"
      style="padding-bottom: 0px;">
        {{ printTitle(singlePost) }}
      </v-card-title>
      <v-card-title
      class="date">
        {{ printDate(singlePost) }}
      </v-card-title>
      <v-card-actions>
      <v-spacer></v-spacer>
      </v-card-actions>
      <v-expand-transition>
      <div v-show="show">
        <v-card-text
        v-html="printFullDescription(singlePost)">
        </v-card-text>
      </div>
    </v-expand-transition>
      </v-card>
    </v-container>
    <v-container
    v-else>
      <h3>Select a feed to begin reading</h3>
    </v-container>
    </v-sheet>
  </v-col>
</template>

<script>
export default {
  data() {
    return {
      postData: this.posts || null,
      show: true,
      singlePost: null,
    };
  },
  methods: {
    showSinglePost(index) {
      this.singlePost = this.postData.posts[index];
      // eslint-disable-next-line
    },
    printTitle(post) {
      return post.querySelector('title').innerHTML;
    },
    printSampleDescription(post) {
      const description = new window
        .DOMParser()
        .parseFromString(post.querySelector('item description').childNodes[0].textContent, 'text/html');
      return description.querySelector('body').innerText;
    },
    printDate(post) {
      const date = new Date(post.querySelector('pubDate').innerHTML);
      return `${date.getMonth() + 1}/${date.getDate()}/${date.getFullYear()}`;
    },
    printImageURL(post) {
      const image = new window
        .DOMParser()
        .parseFromString(post.querySelector('item description').childNodes[0].textContent, 'text/html');
      return image.querySelector('img').src;
    },
    printFullDescription(post) {
      const fullDescription = new window
        .DOMParser()
        .parseFromString(post.querySelector('encoded').childNodes[0].textContent, 'text/html');
      // eslint-disable-next-line
      fullDescription.querySelector('img').remove();
      this.scrollToTop();
      return fullDescription.querySelector('body').innerHTML;
    },
    scrollToTop() {
      // eslint-disable-next-line
      this.$refs.mainContent.$el.scrollTop = 0;
    },
    goBack() {
      this.singlePost = null;
      // eslint-disable-next-line
      this.scrollToTop();
    },
  },
  props: {
    posts: Object,
    back: Boolean,
  },
  watch: {
    posts: {
      handler() {
        // eslint-disable-next-line
        this.goBack();
      },
    },
  },
};
</script>

<style scoped>
  #mainContent > .v-sheet{
    max-height: 80vh;
    overflow: scroll;
  }

  .v-card{
    margin-bottom: 15px;
  }

  .v-card__title{
    word-break: normal;
  }

  .date{
    color: red;
    font-size: 16px;
  }
  #backBtn{
    position: absolute;
    top: -28px;
  }

</style>
