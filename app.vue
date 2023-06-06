<template>
  <!-- Components -->
  <!-- !!!TAKE NOTE!!! -->
  <!-- Navbar is, in fact, volgjebestelling -->
  <Navbar />
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';

import Navbar from './pages/navbar.vue';
import MainPage from './pages/index.vue';

export default {
  components: {
    Navbar,
    MainPage,
  },
};
</script>
