<template>
  <div id="app">
    <router-view />
    <FooterCom />
  </div>
</template>

<script>
import FooterCom from "@/components/FooterCom.vue";
export default {
  components: {
    FooterCom,
  },
};
</script>

<style></style>
