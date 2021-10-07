<template>
  <div id="app" class="container">
    <SourceSelection :source="source" @sourceChanged="handleSourceChange"></SourceSelection>
    <NewsList :source="source"></NewsList>
  </div>
</template>

<script>
import SourceSelection from "./components/SourceSelection";
import NewsList from "./components/NewsList";

export default {
  name: "App",
  components: {
    SourceSelection,
    NewsList,
  },
  data() {
    return {
      source: "",
    };
  },
  methods: {
    handleSourceChange: function (source) {
      this.source = source;
    },
  },
};
</script>

<style>
#app {
  padding-top: 20px;
}
</style>
