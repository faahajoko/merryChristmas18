<template>
  <p>Zeit bis {{ereignis}}: {{countdown}}</p>
</template>

<script>
export default {
  data() {
    return {
      now: null
    };
  },
  props: {
    ereignis: String,
    zielDatum: Number
  },
  computed: {
    countdown: function() {
      const dayInMs = 86400000;
      const hourInMs = 3600000;
      const minInMs = 60000;
      const restZeit = this.zielDatum - this.now;
      const restTage = Math.trunc(restZeit / dayInMs);
      const restStunden = Math.trunc(
        (restZeit - restTage * dayInMs) / hourInMs
      );
      const restMinuten = Math.trunc(
        (restZeit - restTage * dayInMs - restStunden * hourInMs) / minInMs
      );
      const restSekunden = Math.trunc(
        (restZeit -
          restTage * dayInMs -
          restStunden * hourInMs -
          restMinuten * minInMs) /
          1000
      );
      return (
        restTage +
        " Tage " +
        restStunden +
        " Std " +
        restMinuten +
        " Min " +
        restSekunden +
        " Sek "
      );
    }
  },
  beforeMount: function() {
    let self = this;
    setInterval(function() {
      self.now = Date.now();
    }, 1000);
  }
};
</script>

<style>
</style>


