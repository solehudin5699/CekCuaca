<template>
  <div
    :class="
      data.isLoading || Boolean(data.message)
        ? `result_container_loading`
        : `result_container`
    "
  >
    <div v-if="data.isLoading">
      <SpinnerLoader color="rgb(0, 119, 255)" />
    </div>
    <div class="result_content" v-if="data.weather && !data.isLoading">
      <h3 class="result_nameCity">{{ data.name }}, {{ data.sys.country }}</h3>
      <img
        :src="`http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`"
      />
      <h1>{{ condition[data.weather[0].main] }}</h1>
      <h5 class="result_description">"{{ data.weather[0].description }}"</h5>
      <table class="result_table">
        <tr class="result_tableRow">
          <td><h5>Suhu rerata</h5></td>
          <td>
            <h5 class="tableValue">
              {{ data.main.temp }} <span>&#176;C</span>
            </h5>
          </td>
        </tr>
        <tr class="result_tableRow">
          <td><h5>Suhu minimum</h5></td>
          <td>
            <h5 class="tableValue">
              {{ data.main.temp_min }} <span>&#176;C</span>
            </h5>
          </td>
        </tr>
        <tr class="result_tableRow">
          <td><h5>Suhu maksimum</h5></td>
          <td>
            <h5 class="tableValue">
              {{ data.main.temp_max }} <span>&#176;C</span>
            </h5>
          </td>
        </tr>
        <tr class="result_tableRow">
          <td><h5>Tekanan</h5></td>
          <td>
            <h5 class="tableValue">{{ data.main.pressure }} hPa</h5>
          </td>
        </tr>
        <tr class="result_tableRow">
          <td><h5>Kelembapan</h5></td>
          <td>
            <h5 class="tableValue">{{ data.main.humidity }}%</h5>
          </td>
        </tr>
        <tr class="result_tableRow">
          <td><h5>Kecepatan Angin</h5></td>
          <td>
            <h5 class="tableValue">{{ data.wind.speed }} m/s</h5>
          </td>
        </tr>
      </table>
    </div>
    <div v-else-if="data.message && !data.isLoading">
      <h5 class="result_notfound">Kota tidak ditemukan</h5>
    </div>
  </div>
</template>

<script>
import { FacebookLoader, SpinnerLoader } from "vue-spinners-css";
export default {
  name: "Result",
  props: ["data"],
  data() {
    return {
      condition: {
        Thunderstorm: "Hujan badai",
        Drizzle: "Gerimis",
        Rain: "Hujan",
        Snow: "Bersalju",
        Clear: "Cerah",
        Clouds: "Berawan",
        Mist: "Berkabut",
        Smoke: "Berasap",
        Haze: "Berkabut",
        Dust: "Berdebu",
        Fog: "Berkabut",
        Sand: "Berpasir",
        Ash: "Berabu",
        Squall: "Badai",
        Tornado: "Tornado",
      },
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.result_container_loading {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
  height: 65vh;
  padding-top: 15px;
}
.result_container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
  padding-top: 15px;
  padding-bottom: 15px;
}
.result_content {
  background-color: rgba(0, 119, 255, 0.5);
  border-radius: 10px;
  padding: 15px;
  color: #ffffff;
  min-width: 50%;
}
@media screen and (max-width: 768px) {
  .result_content {
    min-width: 90%;
  }
}
.result_nameCity {
  text-align: center;
}
.result_notfound {
  color: rgb(29, 80, 138);
}
.result_description {
  font-style: italic;
  color: rgba(252, 248, 248, 0.829);
  margin-top: -5px;
}
.result_table {
  width: 100%;
}
.result_tableRow {
  color: #ffffff;
}
.tableValue {
  padding-left: 10px;
}
.result_tempAverage {
  position: relative;
}
</style>
