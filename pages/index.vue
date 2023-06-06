<template>
  <div>
    <h1>The current year is:</h1>
    <p>{{ currentYear }}</p>
  </div>
</template>

<script>
//
// Empty line above is to be replaced by "import" statements

export default {
  data() {
    return {
      currentYear: new Date().getFullYear(),
    };
  },
};
</script>
