<template>
  <div id="forecast">
    <table>
      <thead>
        <tr>
          <th colspan="2">Next days</th>
        </tr>
      </thead>
      <tbody>
        <ForecastDay
          v-for="(weather, index) in weathers"
          :key="index"
          :weather="weather"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import ForecastDay from "@/components/ForecastDay.vue";

export default {
  name: "Forecast",
  components: {
    ForecastDay
  },
  props: {
    weathers: Array
  }
};
</script>

<style lang="scss" scoped>
#forecast {
  display: flex;
  flex-flow: row nowrap;
  height: 45vh;
  justify-content: center;
  align-items: center;
  table {
    text-align: left;
    border-collapse: collapse;
    width: 85vw;
    tr {
      th {
        padding: 1.5em;
        text-align: center;
      }
    }
    tr + tr {
      margin-bottom: 20px;
    }
  }
}
</style>
