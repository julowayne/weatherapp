<template>
  <div class="home">
    <Today />
    <Forecast />
  </div>
</template>

<script>
// @ is an alias to /src
import Forecast from "@/components/Forecast.vue";
import Today from "@/components/Today.vue";

export default {
  name: "Home",
  components: {
    Forecast,
    Today
  }
};
</script>
