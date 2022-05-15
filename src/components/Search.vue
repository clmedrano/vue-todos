<template>
  <div id="search-container">
    <input type="text" v-model="query" v-on:input="$emit('query-change', query);" />
  </div>
</template>

<script>
export default {
  name: "SearchssssssssssssName",
  data() {
    return {
      query: "",
    };
  },
};
</script>

<style scope>
#search-container {
  width: 600px;
  margin: 0 auto;
}
input {
  padding: 10px;
  width: 100%;
  outline: none;
}
</style>