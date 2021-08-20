<template>
  <Pagination v-model="page" :maxPage="10" />
</template>

<script>
  import Pagination from "../src/Pagination.vue";

  export default {
    components: {
      Pagination
    },
    data() {
      return {
        page: 3
      }
    }
  };
</script>