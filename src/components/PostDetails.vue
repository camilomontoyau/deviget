<template>
  <v-card class="mx-auto">
    <v-img class="white--text" height="400" :src="image">
      <v-card-title class="align-end fill-height">{{post.title}}</v-card-title>
    </v-img>

    <v-card-text>
      <span>Number of comments {{post.num_comments}}</span>
      <br />
      <span>
        <v-icon>mdi-calendar</v-icon>
        {{dateCreated}}
      </span>
      <br />
      <span>
        <v-icon>mdi-account</v-icon>
        {{post.name}}
      </span>
      <v-divider></v-divider>
      <div
        class="text--primary"
        v-if="post.selftext_html"
        v-html="post.selftext_html"
        style="overflow:scroll"
      ></div>
    </v-card-text>
  </v-card>
</template>

<script>
import _get from "lodash.get";
import moment from "moment";
export default {
  data() {
    return {
      postDetails: null
    };
  },
  computed: {
    image() {
      const { preview = null } = this.$props.post;
      const imageFromPreview = _get(preview, "images.0.source.url", null);
      if (imageFromPreview) {
        return imageFromPreview;
      }
      return require("../assets/reddit-logo.png");
    },
    dateCreated() {
      if (this.$props.post.created) {
        return moment.unix(this.$props.post.created).fromNow();
      }
      return moment.fromNow();
    }
  },
  props: {
    post: { type: Object }
  }
};
</script>