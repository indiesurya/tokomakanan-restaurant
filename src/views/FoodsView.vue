<template>
  <div class="home">
    <Navbar />
    <div class="container mt-3">
      <div class="row mx-1">
        <div class="col-md-9 mb-4">
          <h2>
            <strong>Daftar<span class="primary-text"> Makanan</span></strong>
          </h2>
        </div>
        <div class="col-md-3">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan"
              aria-label="Cari Makanan"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
            <span class="input-group-text" id="basic-addon1"
              ><b-icon-search></b-icon-search
            ></span>
          </div>
        </div>
      </div>
      <div class="row">
        <div
          class="col-md-4 mb-4 justify-content-center d-flex"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "FoodsView",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    getProducts(data) {
      this.products = data;
    },
    searchFood() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.getProducts(response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.getProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>