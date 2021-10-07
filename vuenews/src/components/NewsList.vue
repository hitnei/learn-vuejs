<template>
  <div class="newslist">
    <div class="container">
      <h3 v-show="loading">...Loading</h3>
      <ul v-show="!loading" class="media-list">
        <li class="media" :key="index" v-for="(article, index) in articles">
          <div class="media-left">
            <a :href="article.url" target="_blank">
              <img class="media-object" :src="article.urlToImage" alt="" />
            </a>
          </div>
          <div class="meida-body">
            <h4 class="media-heading">
              <a :href="article.url" target="_blank">{{ article.title }}</a>
              <h5>
                <i>by {{ article.author }}</i>
              </h5>
              <p>{{ article.description }}</p>
            </h4>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "newslist",
  props: ["source"],
  data() {
    return {
      loading: true,
      articles: [],
    };
  },
  methods: {
    updateSource: function async(source) {
      this.loading = true;
      this.$http
        .get(
          `https://newsapi.org/v2/top-headlines?sources=${source.id}&apiKey=b2c5aa5c6363445d83c080a505e25e4e`
        )
        .then((res) => {
          if (res) {
            this.articles = res.body.articles;
          }
          this.loading = false;
        });
    },
  },
  watch: {
    source: function (val) {
      this.updateSource(val);
    },
  },
};
</script>
<style scoped>
.media {
  padding: 10px 0;
}
.media + .media {
  border-top: 1px solid #ccc;
}
.media-left {
  min-width: 128px;
}
.media-object {
  width: 128px;
  padding: 10px;
}
</style>