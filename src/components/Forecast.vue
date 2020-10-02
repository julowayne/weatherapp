<template>
  <div id="forecast">
    <table>
      <thead>
        <tr>
          <th colspan="2">Next days</th>
        </tr>
      </thead>
      <tbody>
        <ForecastDay :temperature="temperature" :weather="weather" />
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
    temperature: [Array, Number],
    weather: String
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
    tr {
      th {
        padding: 1.5em;
        text-align: center;
      }
    }
    text-align: left;
    border-collapse: collapse;
    tr,
    td {
      text-align: center;
      padding: 0.5em;
    }
    tr + tr {
      margin-bottom: 20px;
    }
    width: 85vw;
  }
}
</style>
