<template>
  <v-card class="mx-auto">
    <v-row class="py-4 pl-4">
      <v-col class="shrink">
        <v-img width="100" height="100" :src="image"></v-img>
      </v-col>
      <v-col class="text-center">
        <v-container class="pa-0">
          <v-row>
            <v-col>
              <v-btn icon>
                <v-icon>mdi-heart</v-icon>
              </v-btn>
            </v-col>
            <v-col>
              <v-btn icon>
                <v-icon>mdi-bookmark</v-icon>
              </v-btn>
            </v-col>
            <v-col>
              <v-btn icon>
                <v-icon>mdi-share-variant</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
import _get from "lodash.get";
export default {
  data() {
    return {};
  },
  computed: {
    image() {
      const { preview } = this.$props.post;
      const imageFromPreview = _get(
        preview,
        "images.0.resolutions.0.url",
        null
      );
      if (imageFromPreview) {
        return imageFromPreview;
      }
      return require("../assets/logo.png");
    }
  },
  components: {},
  props: {
    post: { type: Object }
  }
};
</script>