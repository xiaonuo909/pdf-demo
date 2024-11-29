<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'
import jsPDF from 'jspdf';
import html2pdf from 'html2pdf.js'
import Handlebars from "handlebars";
import templateContent from './templates/demo.handlebars?raw';

const data = ref([
  { key: '1', value: 'a' },
  { key: '2', value: 'b' },
  { key: '3', value: 'c' }
])

const templatee = Handlebars.compile(templateContent)
const htmlContent = templatee({ data: data.value })

const clickEvent = async () => {
  // console.log(htmlContent);
  // const pdf = new jsPDF({
  //   format: 'a4', // 设置页面大小为 A4
  //   unit: 'mm', // 设置单位为毫米
  //   orientation: 'p' // 设置页面方向为纵向
  // });
  // pdf.setFontSize(12);
  // pdf.html(htmlContent, {
  //   callback: function (pdf) {
  //     pdf.save('demo.pdf');
  //   }
  // });



  const options = {
    margin: 0.5,
    filename: `demo.pdf`,
    image: { type: 'jpeg', quality: 1.0 },
    html2canvas: { scale: 2, useCORS: true },
    jsPDF: { unit: 'in', format: 'a4', orientation: 'portrait' },
    pagebreak: { mode: 'avoid-all', before: '#page2el' }
  };
  html2pdf().set(options).from(htmlContent).outputPdf().save();

}


</script>

<template>
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
  <p @click="clickEvent">click</p>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
