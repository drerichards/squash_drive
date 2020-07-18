<template>
  <div>
    <em class="text-2xl flex justify-center mt-6">
      <strong class="mr-2">{{ getImpactSum() }}</strong> total individuals
      impacted.
    </em>
    <div class="flex my-4 flex-wrap">
      <div style="{maxWidth: '300px'}" class="w-full md:w-1/2">
        <div
          v-for="(item, i) in impactData.col1"
          :key="item.title"
          class="font-bold px-2 py-4 flex"
          :class="[i % 2 !== 0 ? bkGray : '']"
        >
          <span class="w-3/4">
            {{ item.title }}
          </span>
          <span class="w-1/4 text-center">
            <div v-if="item.quantity !== 0">{{ item.quantity }}</div>
          </span>
        </div>
      </div>
      <div style="{maxWidth: '300px}" class="w-full md:w-1/2">
        <div
          v-for="(item, i) in impactData.col2"
          :key="item.title + i"
          class="font-bold px-2 py-4 flex md:hidden"
          :class="[i % 2 === 0 ? bkGray : '']"
        >
          <span class="w-3/4">
            {{ item.title }}
          </span>
          <span class="w-1/4 text-center">
            <div v-if="item.quantity !== 0">{{ item.quantity }}</div>
          </span>
        </div>
        <div
          v-for="(item, i) in impactData.col2"
          :key="item.title"
          class="font-bold px-2 py-4 hidden md:flex"
          :class="[i % 2 !== 0 ? bkGray : '']"
        >
          <span class="w-3/4">
            {{ item.title }}
          </span>
          <span class="w-1/4 text-center">
            <div v-if="item.quantity !== 0">{{ item.quantity }}</div>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["impactData"],
  data: () => ({
    bkGray: "bg-gray-300",
    sum: ""
  }),
  methods: {
    getImpactSum: function() {
      let sum1;
      let totalSum;
      sum1 = this.impactData.col1.reduce(
        (total, obj) => obj.quantity + total,
        0
      );
      totalSum =
        this.impactData.col2.reduce((total, obj) => obj.quantity + total, 0) +
        sum1;
      return totalSum;
    }
  }
};
</script>

<style lang="scss" scoped></style>
