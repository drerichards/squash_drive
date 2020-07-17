<template>
  <div class="flex mb-10">
    <div class="w-1/4 border">
      <div class="text-center font-bold p-2">Grant Amount</div>
      <div class="bg-gray-400 text-center p-2">
        ${{
          headerData.grantAmount
            .toString()
            .replace(/\B(?=(\d{3})+(?!\d))/g, ",")
        }}
      </div>
    </div>
    <div class="w-1/4 border">
      <div class="text-center font-bold p-2">Funding Spent</div>
      <div class="bg-gray-400 text-center p-2">
        $({{
          headerData.fundingSpent
            .toString()
            .replace(/\B(?=(\d{3})+(?!\d))/g, ",")
        }})
      </div>
    </div>
    <div class="w-1/4 border">
      <div class="text-center font-bold p-2">Project Start Date</div>
      <div class="bg-gray-400 text-center p-2">
        {{ headerData.projectStartDate }}
      </div>
    </div>
    <div class="w-1/4 border">
      <div class="text-center font-bold p-2">Project End Date</div>
      <div class="bg-gray-400 text-center p-2">
        {{ headerData.projectEndDate }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderGrid",
  props: ["headerData"]
};
</script>
