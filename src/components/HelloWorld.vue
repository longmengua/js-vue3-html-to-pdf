<template>
  <div :style="{ width: `${width}px`, height: `${height}px`, border: '1px solid black' }" ref="content">
    <p>{{ message }}</p>
    <button @click="generatePDF">Generate PDF</button>
    <StatisticChart ref="pdf" />
    <h1>我的日記</h1>

    <div class="entry">
      <h2>2024年7月16日</h2>
      <p>今天天氣晴朗，心情非常愉快。</p>
      <p>早上去散步，感受到清新的空氣和和煦的陽光。</p>
      <p class="date">Posted on July 16, 2024</p>
    </div>

    <div class="entry">
      <h2>2024年7月15日</h2>
      <p>今天下雨了，但是我喜歡雨天的氛圍。</p>
      <p>下午和朋友去咖啡店聊天，度過了一個輕鬆的下午。</p>
      <p class="date">Posted on July 15, 2024</p>
    </div>
  </div>
</template>

<script>
import jsPDF from 'jspdf';
import html2canvas from 'html2canvas';

import StatisticChart from './StatisticChart.vue';

export default {
  data() {
    return {
      message: 'Hello, PDF!',
      width: 600,
      height: 800,
    };
  },
  components: {
    StatisticChart
  },
  methods: {
    async generatePDF() {
      const doc = new jsPDF();
      
      // Get the root element of content div
      const element = this.$refs.content;

      // Use html2canvas to capture the element as canvas
      const canvas = await html2canvas(element);
      const imageData = canvas.toDataURL('image/png');

      // Add image to PDF, scaling to fit the page width
      /**
       * 對於寬度：PDF寬度 = （600 / 300）* 72 ≈ 144 點
       * 對於高度：PDF高度 = （1200 / 300) * 72 ≈ 288 點
      */
      const w = (this.width/300) * 105;
      const h = (this.height/300) * 112;
      doc.addImage(imageData, 'PNG', 0, 0, w, h);

      // Save PDF
      doc.save('generated.pdf');
    }
  }
};
</script>

<style>
h1 {
  text-align: center;
  color: #333;
}

.entry {
  background-color: #fff;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 20px;
}

.entry h2 {
  margin-bottom: 10px;
}

.entry p {
  margin-bottom: 5px;
}

.entry .date {
  font-style: italic;
  color: #888;
}
</style>
