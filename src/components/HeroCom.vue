<template>
  <div class="hero">
    <!-- desktop -->
    <div class="d-md-block d-none">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu,</strong> <br />
                In Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorit Anda</p>
              <router-link class="btn btn-success" to="/foods"
                >Pesan <b-icon-arrow-right></b-icon-arrow-right
              ></router-link>
            </div>
          </div>
        </div>
        <div class="col">
          <img src="../assets/image/ilustrasi.png" alt="hero" width="100%" />
        </div>
      </div>
    </div>

    <!-- mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="col">
            <img src="../assets/image/ilustrasi.png" alt="hero" width="100%" />
          </div>
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu,</strong> <br />
                In Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorit Anda</p>
              <router-link class="btn btn-success" to="/foods"
                >Pesan <b-icon-arrow-right></b-icon-arrow-right
              ></router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroCom",
};
</script>

<style></style>
