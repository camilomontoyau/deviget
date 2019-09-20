<template>
  <v-container>
    <v-layout text-center wrap>
      <v-container class="grey lighten-5">
        <v-row>
          <v-col cols="6" sm="6">
            <v-subheader>Posts</v-subheader>
            <post-header
              v-for="(post, index) in posts"
              :post="post"
              :key="`post-header-${index}`"
              @onSelectPost="selectPost"
            />
          </v-col>
          <v-col cols="6" sm="6">
            <v-subheader>Post detail</v-subheader>
          </v-col>
        </v-row>
      </v-container>
    </v-layout>
  </v-container>
</template>

<script>
import PostHeader from "./PostHeader.vue";
export default {
  data() {
    return {
      selectedPost: null
    };
  },
  components: {
    PostHeader
  },
  props: {
    posts: { type: Array }
  },
  methods: {
    selectPost(post) {
      this.selectedPost = { ...post };
    }
  }
};
</script>
