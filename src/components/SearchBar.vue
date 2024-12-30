<template>
  <div>
    <input
      type="text"
      v-model="query"
      @input="onInput"
      placeholder="Search for Campaign"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
    };
  },
  methods: {
    onInput() {
      console.log("Search query: ", this.query);
      this.$emit("onSearch", this.query);  
    },
  },
};
</script>

<style scoped>

input {
  padding: 8px;
  font-size: 1rem;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 100%;
  max-width: 300px;
}
</style>
