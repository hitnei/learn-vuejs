<template>
  <div class="sourceselection">
    <div class="jumbotron">
      <h3 v-show="loading">...Loading</h3>
      <div v-show="!loading">
        <h2 class="mb-3"><i class="bi bi-card-list"></i> News List</h2>
        <h4>Select News Source</h4>
        <select class="form-control custom-select" @change="selectSource">
          <option
            :key="src.id"
            :value="JSON.stringify(src)"
            v-for="src in sources"
          >
            {{ src.name }}
          </option>
        </select>
        <div v-if="source">
          <h6 class="py-4">{{ source.description }}</h6>
          <a :href="source.url" class="btn btn-primary" target="_blank"
            >Go to {{ source.name }} website</a
          >
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "SourceSelection",
  props: ["sourceChanged", "source"],
  data() {
    return {
      loading: true,
      sources: [],
    };
  },
  created: function () {
    this.loading = true;
    this.$http
      .get(
        `https://newsapi.org/v2/top-headlines/sources?language=en&apiKey=b2c5aa5c6363445d83c080a505e25e4e`
      )
      .then((res) => {
        if (res.body) {
          this.sources = res.body.sources;
          this.$emit("sourceChanged", res.body.sources[0] || {});
        }
        this.loading = false;
      });
  },
  methods: {
    selectSource: function (e) {
      this.$emit("sourceChanged", JSON.parse(e.target.value));
    },
  },
};
</script>
<style scoped>
</style>