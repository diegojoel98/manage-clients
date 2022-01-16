<template>
  <HeaderComponent />
  <ManageClients />
  <FooterComponent />
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import ManageClients from "./components/ManageClients.vue";
import FooterComponent from "./components/FooterComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    ManageClients,
    FooterComponent,
  },
};
</script>

<style>
</style>
