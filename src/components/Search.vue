<template>
  <div class="row mt-3 justify-content-end">
    <div class="col-3">
      <input
        type="text"
        v-model="search"
        class="form-control"
        placeholder="Search TODO..."
        @keyup="searchItem" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchItem() {
      this.$emit("searchItem", this.search);
    },
  },
};
</script>

<style></style>
