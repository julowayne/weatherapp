<template>
  <div id="forecast">
    <table>
      <thead>
        <tr>
          <th colspan="2">Next days</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ tomorrow }}</td>
          <td>
            <img src="../assets/clouds.png" alt="cloudy weather" />
          </td>
        </tr>
        <!--   <tr>
          <td>{{ aftertomorrow }}</td>
          <td>
            <img src="../assets/sun.png" alt="cloudy weather" />
          </td>
        </tr>
        <tr>
          <td>{{ nextaftertomorrow }}</td>
          <td>
            <img src="../assets/wind.png" alt="cloudy weather" />
          </td>
        </tr> -->
      </tbody>
    </table>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Forecast",
  props: {
    temperature: Number
  },
  computed: {
    tomorrow() {
      return moment()
        .add(1, "days")
        .format("dddd DD");
    },
    aftertomorrow() {
      return moment()
        .add(2, "days")
        .format("dddd DD");
    },
    nextaftertomorrow() {
      return moment()
        .add(3, "days")
        .format("dddd DD");
    }
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
