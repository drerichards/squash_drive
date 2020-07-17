<template>
  <div>
    <p class="text-2xl font-bold mb-2">Milestones</p>
    <div class="flex my-4">
      <div class="w-1/6 border bg-blue-900">
        <div class="text-center text-white font-bold p-2">Status</div>
      </div>
      <div class="w-1/6 border bg-blue-900">
        <div class="text-center text-white font-bold p-2">Goal</div>
      </div>
      <div class="w-1/6 border bg-blue-900">
        <div class="text-center text-white font-bold p-2">Current</div>
      </div>
      <div class="w-2/6 border bg-blue-900">
        <div class="text-center text-white font-bold p-2">Beneficiary</div>
      </div>
      <div class="w-4/6 border bg-blue-900">
        <div class="text-center text-white font-bold p-2">Benefit</div>
      </div>
    </div>
    <div v-for="(milestone, i) in milestoneData" :key="milestone.question">
      <em class="mt-2 ml-2">{{ i + 1 }}. {{ milestone.question }}</em>
      <div class="flex mt-1 mb-4">
        <div class="w-1/6 border bg-gray-400">
          <div class="text-center font-bold p-2">
            <CheckMark
              class="w-full"
              v-if="
                milestone.current !== 0 && milestone.current >= milestone.goal
              "
            />
          </div>
        </div>
        <div class="w-1/6 border bg-gray-400">
          <div class="text-center font-bold p-2">
            {{ milestone.goal }}
          </div>
        </div>
        <div class="w-1/6 border bg-gray-400">
          <div
            class="text-center font-bold p-2"
            :class="[
              milestone.current === 0
                ? redText
                : milestone.current < milestone.goal
                ? blueText
                : greenText
            ]"
          >
            {{ milestone.current }}
          </div>
        </div>
        <div class="w-2/6 border bg-gray-400">
          <div class="text-center font-bold p-2">
            {{ milestone.beneficiary }}
          </div>
        </div>
        <div class="w-4/6 border bg-gray-400">
          <div class="text-center font-bold p-2">
            {{ milestone.benefit }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CheckMark from "../../assets/images/check.svg";
export default {
  name: "Milestones",
  components: { CheckMark },
  props: ["milestoneData"],
  data: () => ({
    redText: "text-red-600",
    blueText: "text-blue-600",
    greenText: "text-green-600"
  })
};
</script>

<style lang="scss" scoped></style>
