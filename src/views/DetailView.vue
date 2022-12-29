<template>
  <div class="food-detail">
    <NavbarCom />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/foods">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/image/' + product.gambar"
            class="shadow img-fluid"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
            <hr />
          </h2>
          <h4>
            Harga : <strong>{{ product.harga }}</strong>
          </h4>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pesan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
                required
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                class="form-control"
                v-model="pesan.keterangan"
                placeholder="Masukan Keterangan Makanan"
              ></textarea>
            </div>
            <button class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarCom from "@/components/NavbarCom.vue";
import axios from "axios";
export default {
  name: "DetailView",
  components: {
    NavbarCom,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post(
            "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs",
            this.pesan
          )
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$toast.success("Sukses Masuk Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.pesan.products = this.product;
        axios
          .post(
            "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs",
            this.pesan
          )
          .then(() => {
            this.$toast.success("Jumlah Pesanan Harus Diisi", {
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      }
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/donimhmmdf/kulineran/products" +
          this.$route.params.id
      )
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
