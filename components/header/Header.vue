<template>
  <div>
    <div class="flex justify-between mb-10">
      <div>
        <p class="text-5xl font-bold">SquashDrive</p>
        <p class="text-3xl font-bold text-red-600 mb-0">Semi-Annual Report</p>
        <p class="text-2xl">
          {{ new Date().toDateString().slice(4) }}
        </p>
      </div>
      <div>
        <p class="text-2xl font-bold">
          FUND <span class="text-blue-400">II</span>
        </p>
        <p class="text-2xl font-bold">FOUNDATION</p>
      </div>
    </div>
    <HeaderGrid :headerData="headerData" />
  </div>
</template>

<script>
import HeaderGrid from "./HeaderGrid";

export default {
  name: "Header",
  components: { HeaderGrid },
  props: ["headerData"]
};
</script>
