<template>
  <div class="p-12 h-screen">
    <div class="h-full">
      <div
        v-if="showLoading"
        class="h-screen w-screen fixed z-50 bg-black bg-opacity-75 inset-0 flex justify-center items-center flex-col"
      >
        <div>
          <p class="text-3xl font-extrabold text-white mb-2">
            Generating File
          </p>
          <LoadingIcon />
        </div>
      </div>
      <div id="formContent" class="px-6">
        <Header />
        <HeaderGrid :headerData="headerData" />
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
        <Header v-if="showLoading" />
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
import HeaderGrid from "../components/header/HeaderGrid";
import Milestones from "../components/milestones/Milestones";
import Charts from "../components/charts/Charts";
import Impact from "../components/impact/Impact";
import LoadingIcon from "../assets/images/loading_icon.svg";

const chartColors = {
  red: "rgb(255, 99, 132)",
  orange: "rgb(255, 159, 64)",
  yellow: "rgb(255, 205, 86)",
  green: "rgb(75, 192, 192)",
  blue: "rgb(54, 162, 235)",
  purple: "rgb(225, 234, 154)",
  grey: "rgb(201, 203, 207)"
};

export default {
  components: { Header, HeaderGrid, Milestones, Charts, Impact, LoadingIcon },
  data: () => ({
    headerData: {
      grantAmount: 1000000,
      fundingSpent: 540000,
      projectStartDate: "8/15/2018",
      projectEndDate: "6/30/2021"
    },
    showLoading: false,
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
          data: [3000, 4400, 1000, 2500, 1000]
        }
      ]
    },
    ageChartData: {
      labels: ["7-24 years old"],
      datasets: [
        {
          label: "Age",
          backgroundColor: [chartColors.green],
          data: [8200000]
        }
      ]
    },
    genderChartData: {
      labels: ["Men", "Women"],
      datasets: [
        {
          label: "Gender Identity",
          backgroundColor: [chartColors.blue, chartColors.green],
          data: [5100, 3100]
        }
      ]
    },
    socioChartData: {
      labels: ["$30,000 or less", "Subsidized Meals"],
      datasets: [
        {
          label: "Socioeconomic",
          backgroundColor: [chartColors.blue, chartColors.blue],
          data: [3300, 6600]
        }
      ]
    },
    ethnicityChartOptions: {
      responsive: false,
      layout: {
        padding: {
          top: 40,
          bottom: 30,
          left: 35,
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
          offset: function(context) {
            if (context.dataIndex === 1) {
              return -40;
            }
            return -40;
          },
          formatter: function(value, context) {
            if (value === 1) {
              return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} person`;
            }

            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} people`;
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
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} person`;
            }

            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} people`;
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
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} person`;
            }
            return `
              ${context.chart.data.labels[context.dataIndex]}
              ${value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")} people`;
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
          offset: -80,
          font: {
            weight: "bold"
          },
          formatter: function(value, context) {
            if (value === 1) {
              return `${value
                .toString()
                .replace(/\B(?=(\d{3})+(?!\d))/g, ",")} person`;
            }
            return `${value
              .toString()
              .replace(/\B(?=(\d{3})+(?!\d))/g, ",")} people`;
          }
        }
      },
      gridLines: { offsetGridLines: false },
      scales: {
        xAxes: [
          {
            ticks: {
              beginAtZero: true,
              userCallback: function(value, index, values) {
                value = value.toString();
                value = value.split(/(?=(?:...)*$)/);
                value = value.join(",");
                return value;
              }
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
      this.showLoading = true;
      const formContent = document.getElementById("formContent");
      if (process.client) {
        const JsPDF = require("jspdf");
        const html2canvas = require("html2canvas");
        this.$nextTick(() => {
          if (formContent) {
            window.scrollTo(0, 0);

            html2canvas(formContent).then(canvas1 => {
              const pdf = new JsPDF("p", "pt", "a4");

              for (let i = 0; i <= formContent.clientHeight / 1980; i++) {
                const srcImg = canvas1;
                const sX = 0; // origin
                const sY = 2800 * i; // start this many units down for every new page
                const sWidth = 2700;
                const sHeight = 2800;
                const dX = 0;
                const dY = 0;
                const dWidth = 2020;
                const dHeight = 2200;

                const onePageCanvas = document.createElement("canvas");
                onePageCanvas.setAttribute("width", 2800);
                onePageCanvas.setAttribute("height", 2800);
                const ctx = onePageCanvas.getContext("2d");

                ctx.drawImage(
                  srcImg,
                  sX,
                  sY,
                  sWidth,
                  sHeight,
                  dX,
                  dY,
                  dWidth,
                  dHeight
                );

                const canvasDataURL = onePageCanvas.toDataURL("image/png", 1.0);
                const width = onePageCanvas.width;
                const height = onePageCanvas.clientHeight;

                // add another page if > 1
                if (i > 0) {
                  pdf.addPage(595, 791); //8.5" x 11" in pts (in*72)
                }
                pdf.setPage(i + 1);
                pdf.addImage(
                  canvasDataURL,
                  "PNG",
                  20, // padding
                  20, // padding
                  width * 0.28, // zoom
                  height * 0.28
                );
              }
              pdf.save("SquashDrive_semiannual_report.pdf");
              this.showLoading = false;
            });
          }
        });
      }
    }
  }
};
</script>
