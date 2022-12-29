<template>
  <div class="keranjang">
    <NavbarCom :updateKeranjangs="keranjangs" />
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/image/' + keranjang.products.gambar"
                      class="shadow img-fluid"
                      width="250"
                    />
                  </td>
                  <td>{{ keranjang.products.nama }}</td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td>{{ keranjang.jumlah_pemesanan }}</td>
                  <td>Rp. {{ keranjang.products.harga }}</td>
                  <td>
                    <strong
                      >Rp.
                      {{
                        keranjang.products.harga * keranjang.jumlah_pemesanan
                      }}</strong
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga : </strong>
                  </td>
                  <td>
                    <strong align="right">Rp. {{ totalharga }}</strong>
                  </td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="nama">Nama</label>
              <textarea
                class="form-control"
                placeholder="Masukan Nama"
                v-model="pesan.nama"
              ></textarea>
            </div>
            <div class="form-group">
              <label for="nomor_meja">Nomor Meja</label>
              <input
                type="number"
                v-model="pesan.noMeja"
                class="form-control"
              />
            </div>
            <button class="btn btn-success float-right" @click="checkout">
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
  name: "KeranjangView",
  components: {
    NavbarCom,
  },
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete(
          "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs/" +
            id
        )
        .then(() => {
          this.$toast.success("Sukses Hapus Pesanan", {
            type: "error",
            duration: 3000,
            dismissible: true,
          });
          axios
            .get(
              "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs"
            )
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
        })
        .catch((error) => console.log(error));
    },
    checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.keranjangs = this.keranjangs;
        axios
          .post(
            "https://my-json-server.typicode.com/donimhmmdf/kulineran/pesanans",
            this.pesan
          )
          .then(() => {
            this.keranjangs.map(function (item) {
              axios
                .delete(
                  "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs/" +
                    item.id
                )
                .catch((error) => console.log(error));
            });

            this.$router.push({ path: "/pesanan-sukses" });
            this.$toast.success("Sukses Dipesan", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$toast.success("Nama dan Nomor Meja harus diisi", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/donimhmmdf/kulineran/keranjangs"
      )
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    totalharga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style></style>
