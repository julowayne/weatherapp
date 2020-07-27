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
          <td>07.25</td>
          <td>
            <img src="../assets/cloud.png" alt="cloudy weather" />
          </td>
        </tr>
        <tr>
          <td>07.26</td>
          <td>
            <img src="../assets/sun.png" alt="cloudy weather" />
          </td>
        </tr>
        <tr>
          <td>07.27</td>
          <td>
            <img src="../assets/wind.png" alt="cloudy weather" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Forecast"
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
