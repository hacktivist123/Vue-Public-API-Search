<template>
  <div class="hello">
    <h1 id="center-two">Vue Public API Search</h1>
    <input v-model="term" type="search" id="center" />
    <button @click="search" id="search">Search</button>
    <h3>
      Just Search for any Popular Product API with either its intials or
      fullname e.g Youtube or Y
    </h3>
    <div v-if="results">
      <ul>
        <li v-for="result in results" :key="result.Link">
          <a :href="result.Link" target="_new">{{ result.API }}</a> -
          {{ result.Description }}
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "Search",
  data() {
    return {
      term: "",
      results: null
    };
  },
  methods: {
    search() {
      if (this.term.trim() === "") return;
      fetch(
        `https://api.publicapis.org/entries?title=${encodeURIComponent(
          this.term
        )}`
      )
        .then(res => res.json())
        .then(res => {
          this.results = res.entries;
        });
    }
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#search {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  padding-left: 0.1rem;
  color: red;
}

#center-two {
  position: relative;
}
</style>
