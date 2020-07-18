<template>
  <div>
    <p class="text-2xl font-bold my-4 mt-12">Demographics</p>

    <div
      class="flex flex-wrap justify-center md:justify-around items-center mb-6"
    >
      <div class="min-w-screen-sm">
        <p class="text-center font-bold">Ethnicity</p>
        <DoughnutChart
          :data="ethnicityChartData"
          :options="ethnicityChartOptions"
          :height="250"
        />
      </div>
      <div class="min-w-screen-sm">
        <p class="text-center font-bold">Age</p>
        <DoughnutChart
          :data="ageChartData"
          :options="ageChartOptions"
          :height="250"
        />
      </div>
    </div>
    <div class="flex flex-wrap justify-center md:justify-around items-center">
      <div class="min-w-screen-sm">
        <p class="text-center font-bold">Gender Identity</p>
        <DoughnutChart
          :data="genderChartData"
          :options="genderChartOptions"
          :height="250"
        />
      </div>
      <div class="min-w-screen-sm">
        <p class="text-center font-bold">Socioeconomic</p>
        <HorizontalBar
          :data="socioChartData"
          :options="socioChartOptions"
          :height="250"
        />
      </div>
    </div>
  </div>
</template>

<script>
import DoughnutChart from "./DoughnutChart";
import HorizontalBar from "./HorizontalBar";
import "chartjs-plugin-datalabels";
export default {
  components: { DoughnutChart, HorizontalBar },
  props: [
    "ethnicityChartData",
    "ethnicityChartOptions",
    "ageChartData",
    "ageChartOptions",
    "genderChartData",
    "genderChartOptions",
    "socioChartData",
    "socioChartOptions"
  ]
};
</script>

<style lang="scss" scoped></style>
