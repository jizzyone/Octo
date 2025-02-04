<script>
import Card from "@/components/Card.vue";

export default {
  name: "Main",
  components: {Card},
  data() {
    return {
      isSmallScreen: window.innerWidth < 640,
      isMediumScreen: window.innerWidth < 1024,
      currentIndex: 0,
      items: [
        {
          id: 1,
          category: 'MARKETING',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based',
          buttonText: 'Call to action'
        },
        {
          id: 2,
          category: 'MARKETING',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based'
        },
        {
          id: 3,
          category: 'DEVELOPMENT',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based'
        },
        {
          id: 4,
          category: 'MARKETING',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based'
        },
        {
          id: 5,
          category: 'DEVELOPMENT',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based'
        },
        {
          id: 6,
          category: 'MARKETING',
          image: '/sakura.jpg',
          author: 'Adam Sandler',
          title: 'Solutions for people like you',
          description: 'How can we help your technology and services business develop a revenue engine based'
        },
      ]
    }
  },
  methods: {
    prev() {
      this.currentIndex = this.currentIndex > 0 ? this.currentIndex - 1 : this.chunkedItems.length - 1;
    },
    next() {
      this.currentIndex = this.currentIndex < this.chunkedItems.length - 1 ? this.currentIndex + 1 : 0;
    },
    handleResize() {
      this.isSmallScreen = window.innerWidth < 640;
      this.isMediumScreen = window.innerWidth < 1024;
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
  },
  computed: {
    chunkedItems() {
      const chunks = [];
      const chunkSize = window.innerWidth < 768 ? 1 : window.innerWidth < 1024 ? 2 : 3;
      for (let i = 0; i < this.items.length; i += chunkSize) {
        chunks.push(this.items.slice(i, i + chunkSize));
      }
      return chunks;
    }
  }
}
</script>

<template>
  <!-- Верхний блок -->
  <div class="w-full h-48 md:h-56 lg:h-64 overflow-hidden relative">
    <img src="/sakura.jpg" alt="sakura" class="w-full h-full object-cover object-top">
    <div class="absolute inset-0 backdrop-blur-sm bg-black bg-opacity-30"></div>
    <h2 class="text-3xl md:text-4xl lg:text-5xl w-full md:w-[600px] lg:w-[800px] text-center text-white font-semibold absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 px-4">
      Solutions for people like you
    </h2>
  </div>

  <!-- Карточки -->
  <div class="flex justify-center px-4">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 py-12 w-full max-w-7xl">
      <template v-for="(item, index) in items" :key="item.id">
        <Card v-if="index < (isSmallScreen ? 2 : isMediumScreen ? 4 : 6)" v-bind="item" />
      </template>
    </div>
  </div>

  <!-- Черная секция -->
  <div class="flex flex-col lg:flex-row justify-between p-8 md:p-16 lg:p-24 bg-black gap-8">
    <div class="flex flex-col gap-6 max-w-2xl">
      <h3 class="text-4xl md:text-5xl lg:text-7xl text-cyan-500 font-semibold">Solutions for people like you</h3>
      <span class="text-xl md:text-2xl lg:text-3xl text-white">How can we help your technology and services business develop a revenue engine based on Hubspot?</span>
      <div class="flex flex-col md:flex-row gap-4">
        <button class="bg-cyan-500 text-white py-4 px-8 lg:px-12">Call to action</button>
        <button class="border-2 border-cyan-500 text-white py-4 px-8 lg:px-12">Call to action</button>
      </div>
    </div>
    <div class="w-full lg:w-auto">
      <img src="/canon.jpg" alt="" class="w-full lg:w-auto">
    </div>
  </div>
  <!-- Нижний слайдер -->
  <div class="slider-container relative mx-auto px-4 py-12 w-full max-w-7xl">
    <div class="overflow-hidden">
      <div class="flex transition-transform duration-500"
           :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div v-for="chunk in chunkedItems" :key="chunk[0].id"
             class="w-full flex-none px-4">
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            <div v-for="item in chunk" :key="item.id"
                 class="bg-white rounded-lg shadow-lg overflow-hidden">
              <Card v-bind="item" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="flex justify-center gap-4 mt-6 text-4xl text-cyan-500">
      <button @click="prev">&lt;</button>
      <button @click="next">&gt;</button>
    </div>
  </div>
</template>

<style scoped>
</style>
