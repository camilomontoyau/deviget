<template>
  <v-container>
    <v-layout text-center wrap>
      <v-container class="grey lighten-5">
        <v-row>
          <v-col cols="6" sm="12" md="6">
            <v-subheader>Posts</v-subheader>
            <v-banner :sticky="true">
              <div class="scrollable">
                <post-header
                  v-for="(post, index) in posts"
                  :post="post"
                  :key="`post-header-${index}-${post.id}`"
                  :postindex="index"
                  @onSelectPost="selectPost"
                />
                <v-divider></v-divider>
                <v-btn color="green" :disabled="!showMore" @click="fetchMore">more posts</v-btn>
              </div>
            </v-banner>
          </v-col>
          <v-col cols="6" sm="12" md="6">
            <v-subheader>Post detail</v-subheader>
            <post-details v-if="selectedPost" :post="selectedPost" />
          </v-col>
        </v-row>
      </v-container>
    </v-layout>
  </v-container>
</template>

<script>
import PostHeader from "./PostHeader.vue";
import PostDetails from "./PostDetails.vue";
export default {
  data() {
    return {
      selectedPost: null
    };
  },
  computed: {
    showMore() {
      return this.$props.length % 50 === 0 || this.$props.page === 1;
    }
  },
  components: {
    PostHeader,
    PostDetails
  },
  props: {
    posts: { type: Array },
    page: { type: Number, default: 1 }
  },
  methods: {
    selectPost({ post, index }) {
      this.selectedPost = { ...post };
      this.$emit("onReadPost", { index });
    },
    fetchMore() {
      this.$emit("onFetchMore");
    }
  }
};
</script>
<style scoped>
.scrollable {
  max-height: 34em;
  overflow-y: scroll;
}
</style>
