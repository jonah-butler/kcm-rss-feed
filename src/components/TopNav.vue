<template>
  <v-app-bar
  app
  color="white"
  flat
  >
  <v-container class="py-0 fill-height">
    <v-avatar
      class="mr-10"
      color="grey darken-1"
      size="52"
    >
    <v-img
    v-if="!avatar"
    src="@/assets/computer.png">
    </v-img>
    <v-img
    v-else
    src="avatar">
    </v-img>
    </v-avatar>
    <v-spacer></v-spacer>
    <h2>KCM RSS Feed</h2>
  </v-container>
</v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      avatar: null,
    };
  },
  props: {
    image: String,
  },
};
</script>

<style>

</style>
