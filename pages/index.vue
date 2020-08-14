<template>
  <div class="p-12 h-screen">
    <div class="h-full">
      <div id="formContent1" class="px-6">
        <Header :headerData="headerData" />
        <Milestones :milestoneData="milestoneData" />
        <Charts
          :ethnicityChartData="ethnicityChartData"
          :ethnicityChartOptions="ethnicityChartOptions"
          :ageChartData="ageChartData"
          :ageChartOptions="ageChartOptions"
          :genderChartData="genderChartData"
          :genderChartOptions="genderChartOptions"
          :socioChartData="socioChartData"
          :socioChartOptions="socioChartOptions"
        />
      </div>
      <div id="formContent2" class="px-6">
        <Impact :impactData="impactData" />
      </div>
      <no-ssr>
        <button
          class="bg-green-300 hover:bg-green-400 text-gray-800 font-bold py-2 px-4 border-l border-r border-gray-400 mb-12"
          @click="generatePDF()"
        >
          Print Form
        </button>
      </no-ssr>
    </div>
  </div>
</template>

<script>
import Header from "../components/header/Header";
import Milestones from "../components/milestones/Milestones";
import Charts from "../components/charts/Charts";
import Impact from "../components/impact/Impact";

const chartColors = {
  red: "rgb(255, 99, 132)",
  orange: "rgb(255, 159, 64)",
  yellow: "rgb(255, 205, 86)",
  green: "rgb(75, 192, 192)",
  blue: "rgb(54, 162, 235)",
  purple: "rgb(153, 102, 255)",
  grey: "rgb(201, 203, 207)"
};

export default {
  components: { Header, Milestones, Charts },
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
    ],
    impactData: {
      col1: [
        { title: "Pre-K to 3rd Grade", quantity: 8 },
        { title: "Grades 4-8", quantity: 83 },
        { title: "Grades 9-12", quantity: 29 },
        { title: "Home Schooling", quantity: 0 },
        { title: "Private Schools", quantity: 7 },
        { title: "Music Education", quantity: 0 },
        { title: "High School Internships", quantity: 2 },
        { title: "Mentors", quantity: 0 },
        { title: "Advanced Placement", quantity: 5 },
        { title: "Military Schools", quantity: 0 },
        { title: "Community Colleges", quantity: 0 },
        { title: "Online Colleges", quantity: 0 },
        { title: "HBCUs", quantity: 1 }
      ],
      col2: [
        { title: "Scholarships", quantity: 4 },
        { title: "Internships", quantity: 0 },
        { title: "Mentors", quantity: 0 },
        { title: "Fellows & Post Grads", quantity: 0 },
        { title: "Workforce Prep", quantity: 0 },
        { title: "Trainees", quantity: 0 },
        { title: "Placements", quantity: 0 },
        { title: "Middle Management", quantity: 0 },
        { title: "Upper Management", quantity: 0 },
        { title: "C-Suite", quantity: 0 },
        { title: "Training", quantity: 0 },
        { title: "Startups", quantity: 0 },
        { title: "Ownership", quantity: 0 }
      ]
    },
    ethnicityChartData: {
      labels: [
        "Asian American",
        "Hispanic or Latinx",
        "White or European American",
        "Black or African American",
        "Mixed"
      ],
      datasets: [
        {
          backgroundColor: [
            chartColors.green,
            chartColors.yellow,
            chartColors.red,
            chartColors.blue,
            chartColors.purple
          ],
          data: [3, 44, 1, 25, 10]
        }
      ]
    },
    ageChartData: {
      labels: ["7-24 years old"],
      datasets: [
        {
          label: "Age",
          backgroundColor: [chartColors.green],
          data: [82]
        }
      ]
    },
    genderChartData: {
      labels: ["Men", "Women"],
      datasets: [
        {
          label: "Gender Identity",
          backgroundColor: [chartColors.blue, chartColors.green],
          data: [51, 31]
        }
      ]
    },
    socioChartData: {
      labels: ["$30,000 or less", "Subsidized Meals"],
      datasets: [
        {
          label: "Socioeconomic",
          backgroundColor: [chartColors.blue, chartColors.blue],
          data: [33, 66]
        }
      ]
    },
    ethnicityChartOptions: {
      responsive: false,
      layout: {
        padding: {
          top: 50,
          bottom: 50,
          left: 55,
          right: 10
        }
      },
      legend: {
        display: false
      },
      title: {
        display: false
      },
      plugins: {
        datalabels: {
          display: true,
          anchor: "center",
          clamp: true,
          align: "end",
          offset: function(context) {
            if (context.dataIndex === 1) {
              return -40;
            }
            return 20;
          },
          formatter: function(value, context) {
            if (value === 1) {
              return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} person`;
            }

            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} people`;
          }
        }
      }
    },
    ageChartOptions: {
      responsive: false,
      layout: {
        padding: {
          top: 10,
          bottom: 50,
          left: 55,
          right: 10
        }
      },
      legend: {
        display: false
      },
      title: {
        display: false
      },
      plugins: {
        datalabels: {
          display: true,
          anchor: "end",
          clamp: true,
          align: "end",
          offset: -15,
          formatter: function(value, context) {
            if (value === 1) {
              return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} person`;
            }

            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} people`;
          }
        }
      }
    },
    genderChartOptions: {
      responsive: false,
      layout: {
        padding: {
          top: 10,
          bottom: 50,
          left: 55,
          right: 30
        }
      },
      legend: {
        display: false
      },
      title: {
        display: false
      },
      plugins: {
        datalabels: {
          display: true,
          anchor: "end",
          clamp: true,
          align: "end",
          offset: function(context) {
            if (context.dataIndex === 0) {
              return -50;
            }
            return 10;
          },
          formatter: function(value, context) {
            if (value === 1) {
              return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} person`;
            }
            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value} people`;
          }
        }
      }
    },
    socioChartOptions: {
      responsive: false,
      layout: {
        padding: {
          top: 10,
          bottom: 50,
          left: 55,
          right: 30
        }
      },
      legend: {
        display: false
      },
      title: {
        display: false
      },
      plugins: {
        datalabels: {
          color: "white",
          display: true,
          anchor: "end",
          clamp: true,
          align: "end",
          offset: -65,
          font: {
            weight: "bold"
          },
          formatter: function(value, context) {
            if (value === 1) {
              return `${value} person`;
            }
            return `${value} people`;
          }
        }
      },
      gridLines: { offsetGridLines: false },
      scales: {
        xAxes: [
          {
            ticks: {
              beginAtZero: true
            }
          }
        ],
        yAxes: [
          {
            ticks: {
              beginAtZero: true
            },
            gridLines: {
              display: false
            }
          }
        ]
      }
    }
  }),
  methods: {
    generatePDF: function() {
      if (process.client) {
        const JsPDF = require("jspdf");
        const html2canvas = require("html2canvas");
        const formContent1 = document.getElementById("formContent1");
        const formContent2 = document.getElementById("formContent2");

        this.$nextTick(() => {
          window.scrollTo(0, 0);
          const pdf = new JsPDF("p", "mm", "a4");

          html2canvas(formContent1).then(canvas1 => {
            const ratio = canvas1.width / canvas1.height;
            const width = pdf.internal.pageSize.getWidth() - 20;
            const height = width / ratio;
            pdf.addImage(canvas1, "PNG", 10, 10, width, height);
            pdf.autoPrint();
            pdf.output("dataurlnewwindow");
          });
          this.$nextTick(() => {
            html2canvas(formContent2).then(canvas2 => {
              const pdf = new JsPDF("p", "mm", "a4");
              const ratio = canvas2.width / canvas2.height;
              const width = pdf.internal.pageSize.getWidth() - 20;
              const height = width / ratio;
              pdf.addImage(canvas1, "PNG", 100, 10, width, height);
              // pdf.save();
              // console.log(pdf);
            });
          });
          // this.$nextTick(() => {
          //   pdf.save();
          // });
        });
      }
    }
  }
};
</script>
