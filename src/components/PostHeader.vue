<template>
  <v-card class="mx-auto">
    <v-row>
      <v-col class="shrink">
        <a :href="image" target="_blank">
          <v-img width="100" height="100" :src="image" />
        </a>
      </v-col>
      <v-col class="text-center">
        <v-row>
          <v-col>
            <a @click.prevent="selectPost">{{post.title}}</a>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-icon>mdi-account</v-icon>

            {{post.name}}
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col md="4">comments {{post.num_comments}}</v-col>
      <v-col md="6">
        <v-icon>mdi-calendar</v-icon>
        {{dateCreated}}
      </v-col>
      <v-col md="2">
        <v-btn v-if="post.readStatus" icon>
          <v-icon>mdi-eye-check</v-icon>
        </v-btn>
        <v-btn v-else icon>
          <v-icon>mdi-eye-outline</v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
import _get from "lodash.get";
import moment from "moment";
export default {
  data() {
    return {};
  },
  computed: {
    image() {
      const { preview = null } = this.$props.post;
      const imageFromPreview = _get(
        preview,
        "images.0.resolutions.0.url",
        null
      );
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
  components: {},
  props: {
    post: { type: Object },
    postindex: { type: Number }
  },
  methods: {
    selectPost() {
      this.$emit("onSelectPost", {
        post: this.$props.post,
        index: this.$props.postindex
      });
    }
  }
};
</script>