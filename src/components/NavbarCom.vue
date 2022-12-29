<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <!-- <div class="container-fluid"> -->
      <a class="navbar-brand" href="#">Kulineran</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/keranjang">
              Keranjang
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2">{{
                updateKeranjangs
                  ? updateKeranjangs.length
                  : jumlah_pesanans.length
              }}</span>
            </router-link>
          </li>
        </ul>
      </div>
      <!-- </div> -->
    </div>
  </nav>
</template>

<script>
import axios from "axios";
export default {
  name: "NavbarCom",
  data() {
    return {
      jumlah_pesanans: [],
    };
  },
  props: ["updateKeranjangs"],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanans = data;
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs"
      )
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
