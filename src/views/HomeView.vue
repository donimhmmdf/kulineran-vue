<template>
  <div class="home">
    <NavbarCom />
    <div class="container">
      <HeroCom />
      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right"
            >Lihat Semua <b-icon-eye></b-icon-eye
          ></router-link>
        </div>
      </div>
      <div class="row mb-3">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProductCom :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavbarCom from "@/components/NavbarCom.vue";
import HeroCom from "@/components/HeroCom.vue";
import CardProductCom from "@/components/CardProductCom.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    NavbarCom,
    HeroCom,
    CardProductCom,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/donimhmmdf/kulineran/best-products"
      )
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
