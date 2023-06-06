<template>
  <router-link to="pages/index.vue">Index.vue</router-link>
  <Navbar />
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';

import Navbar from './pages/navbar.vue';

export default {
  components: {
    Navbar,
  },
};
</script>
