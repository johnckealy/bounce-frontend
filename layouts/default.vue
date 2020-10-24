<template>
  <div>
    <Navbar />
    <Nuxt />
  </div>
</template>


<script>
import Navbar from "../components/Navbar.vue";

export default {
  name: "courts",
  components: {
    Navbar,
  },
};
</script>