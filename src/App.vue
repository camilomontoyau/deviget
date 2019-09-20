<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Top</span>
        <span class="font-weight-light">Reddit posts</span>
      </v-toolbar-title>
    </v-app-bar>
    <v-content>
      <maincontent :posts="myListing" />
    </v-content>
  </v-app>
</template>

<script>
import snoowrap from "snoowrap";
import Maincontent from "./components/Maincontent.vue";

const r = new snoowrap({
  userAgent: "deviget-test2",
  clientId: "TIPuc7DsPEgEwA",
  clientSecret: "QtIYW3DpMwbXCjfJeFONI_8fyxk",
  refreshToken: "81058191780-23buKHuO4lGTricyV5L6xI1yOAY"
});

let currentListing = null;

export default {
  name: "App",
  components: { Maincontent },
  data() {
    return { myListing: [], page: 1 };
  },
  methods: {
    getTop() {
      r.getTop({ limit: 50 }).then(resultListing => {
        currentListing = resultListing;
        this.myListing = resultListing.map(
          ({
            title = null,
            author: { name = null },
            created = null,
            num_comments = null,
            thumbnail = null,
            preview = null
          }) => ({ title, name, created, num_comments, thumbnail, preview })
        );
      });
    },
    fetchMore() {
      this.page = this.page++;
      currentListing.fetchMore({ amount: 50 }).then(extendedListing => {
        currentListing = extendedListing;
        this.myListing = extendedListing.map(
          ({
            title = null,
            author: { name = null },
            created = null,
            num_comments = null,
            thumbnail = null,
            preview = null
          }) => ({ title, name, created, num_comments, thumbnail, preview })
        );
      });
    }
  },
  beforeMount() {
    this.getTop();
  }
};
</script>
