<template>
  <v-col>
    <v-sheet
    min-height="70vh"
    rounded="lg"
    >
    <v-container
    v-if="posts && posts.length">
      <v-row dense>
        <v-col cols="12">
          <v-card
            color="#385F73"
            dark
          >
            <v-card-title class="text-h5">
              Unlimited music now
            </v-card-title>

            <v-card-subtitle>Listen to your favorite artists and albums</v-card-subtitle>

            <v-card-actions>
              <v-btn text>
                Listen Now
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
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
  props: {
    posts: Array,
  },
};
</script>

<style scoped>
  .v-sheet{
    max-height: 80vh;
    overflow: scroll;
  }

</style>
