<template>
  <p>Zeit bis {{ereignis}}: {{countdown}}</p>
</template>

<script>
export default {
  props: {
    ereignis: "",
    zielDatum: ""
  },
  computed: {
    countdown: function() {
      let timeLeft;
    }
  }
};
</script>

<style>
</style>


