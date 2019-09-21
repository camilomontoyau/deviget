<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Top</span>
        <span class="font-weight-light">Reddit posts</span>
      </v-toolbar-title>
    </v-app-bar>
    <v-content>
      <maincontent
        :posts="myListing"
        @onFetchMore="fetchMore"
        :page="page"
        @onReadPost="markPostAsRead"
      />
    </v-content>
  </v-app>
</template>

<script>
import Maincontent from "./components/Maincontent.vue";
import r from "./services/reddit";

let currentListing = null;

const normalizePost = ({
  title = null,
  author: { name = null },
  created = null,
  num_comments = null,
  preview = null,
  id = null,
  selftext_html = null
}) => ({
  title,
  name,
  created,
  num_comments,
  preview,
  readStatus: false,
  id,
  selftext_html
});

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
        this.myListing = resultListing.map(normalizePost);
      });
    },
    fetchMore() {
      this.page = this.page + 1;
      currentListing.fetchMore({ amount: 50 }).then(extendedListing => {
        currentListing = extendedListing;
        this.myListing = extendedListing.map(normalizePost);
      });
    },
    markPostAsRead({ index }) {
      this.myListing[index].readStatus = true;
    }
  },
  beforeMount() {
    this.getTop();
  }
};
</script>
