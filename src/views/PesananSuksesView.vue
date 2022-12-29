<template>
  <div class="pesanan-sukses">
    <NavbarCom />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="../assets/image/menunggu.png" alt="" width="300" />
          <h2>
            <strong>Sukses!!!</strong>
          </h2>
          <h4>
            Pesanan anda akan segera diproses <br />
            Mohon ditunggu
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarCom from "@/components/NavbarCom.vue";
export default {
  components: {
    NavbarCom,
  },
};
</script>

<style></style>
