<template>
  <el-container class="el-container">
  <Product />
</el-container>
</template>

<script>
// @ is an alias to /src
import Product from "../components/Product.vue";

export default {
  name: "Home",
  components: {
    Product,
  },
};
</script>
