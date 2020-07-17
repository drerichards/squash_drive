<template>
  <div class="p-12 h-screen">
    <div class="h-full">
      <Header :headerData="headerData" />
      <Milestones :milestoneData="milestoneData" />
    </div>
  </div>
</template>

<script>
import Header from "../components/header/Header";
import Milestones from "../components/milestones/Milestones";
export default {
  components: { Header, Milestones },
  data: () => ({
    headerData: {
      grantAmount: 1000000,
      fundingSpent: 540000,
      projectStartDate: "8/15/2018",
      projectEndDate: "6/30/2021"
    },
    milestoneData: [
      {
        question: "Establish benchmarks that show STEM mastery",
        goal: 0,
        current: 0,
        beneficiary: "students",
        benefit: "surveyed"
      },
      {
        question:
          "During the school year, deliver an average of 90 minutes per week of STEM programming",
        goal: 90,
        current: 90,
        beneficiary: "students",
        benefit: "instructed for 90 minutes per week"
      },
      {
        question: "Deliver an average of 5 weeks of intensive STEM camps",
        goal: 96,
        current: 82,
        beneficiary: "students",
        benefit: "attended 5-weeks of STEM camp"
      },
      {
        question: "Enroll 80% of students in external STEM opporunities",
        goal: 66,
        current: 20,
        beneficiary: "students",
        benefit: "received external STEM opportunities"
      }
    ]
  })
};
</script>
