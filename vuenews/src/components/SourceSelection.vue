<template>
  <div class="sourceselection">
    <div class="jumbotron">
      <h2 class="mb-3"><i class="bi bi-card-list"></i> News List</h2>
      <h4>Select News Source</h4>
      <select class="form-control custom-select" @change="sourceChange">
        <option :key="src.id" :value="src.id" v-for="src in sources">
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
</template>
<script>
export default {
  name: "SourceSelection",
  data() {
    return {
      sources: [],
      source: "",
    };
  },
  created: function () {
    this.$http
      .get(
        `https://newsapi.org/v2/top-headlines/sources?language=en&apiKey=b2c5aa5c6363445d83c080a505e25e4e`
      )
      .then((res) => {
        this.sources = res.data.sources;
        if (this.sources.length > 0) this.source = this.sources[0];
      });
  },
  methods: {
    sourceChange: function (e) {
      this.source = this.sources.find((s) => s.id === e.target.value);
    },
  },
};
</script>
<style scoped>
</style>