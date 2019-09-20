<template>
  <v-card class="mx-auto">
    <v-row>
      <v-col class="shrink">
        <a :href="image" target="_blank">
          <v-img width="100" height="100" :src="image" />
        </a>
      </v-col>
      <v-col class="text-center">
        <v-container class="pa-0">
          <v-row>
            <v-col>
              <v-card-title>{{post.title}}</v-card-title>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <v-card-actions>
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
              </v-card-actions>
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
      const { preview = null } = this.$props.post;
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