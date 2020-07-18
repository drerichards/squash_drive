<template>
  <div class="w-full inline-flex justify-end mb-4">
    <button
      class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l"
      @click="generatePDF('email')"
    >
      Email Form
    </button>
    <button
      class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 border-l border-r border-gray-400"
      @click="generatePDF('print')"
    >
      Print Form
    </button>
    <button
      class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r"
      @click="generatePDF('download')"
    >
      Download Form
    </button>
  </div>
</template>

<script>
export default {
  data: () => ({}),
  methods: {
    generatePDF(selectedMethod) {
      this.pdfMethod = selectedMethod;
      if (process.client) {
        const JsPDF = require("jspdf");
        const html2canvas = require("html2canvas");
        const contentHtml = document.getElementById("pdf-content");
        this.$nextTick(() => {
          window.scrollTo(0, 0);
          html2canvas(contentHtml).then(canvas => {
            const pdf = new JsPDF("p", "mm", "a4");
            const ratio = canvas.width / canvas.height;
            const width = pdf.internal.pageSize.getWidth() - 20;
            const height = width / ratio;
            pdf.addImage(canvas, "PNG", 10, 10, width, height);
            switch (this.pdfMethod) {
              case "email":
                const pdfURIOutput = pdf.output();
                this.emailPDF(pdfURIOutput);
                break;
              case "print":
                pdf.autoPrint();
                pdf.output("dataurlnewwindow");
                break;
              case "download":
                pdf.save("certificate_of_attendance.pdf");
                break;
              default:
                break;
            }
            this.pdfMethod = null;
          });
        });
      }
    },
    async emailPDF(pdfURI) {
      try {
        const encodedData = window.btoa(pdfURI);
        await axios.post("/send-email", {
          email: this.email,
          attachment: encodedData
        });
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>
