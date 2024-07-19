<template>
  <div class="bg-[#FF4863] text-white p-5 rounded-lg max-w-sm font-sans">
    <div class="flex">
      <h2 class="text-lg font-bold mb-2">チャット先を指定</h2>
      <button class="ml-auto"><img src="/images/indent.svg" class="invert w-6"></button>
    </div>
    <p class="text-sm mb-4">チャット先が指定されていません。</p>

    <div class="bg-gray-800 rounded flex items-center p-2 mb-3">
      <span class="mr-2"><img src="/images/link.svg" class="invert w-6"></span>
      <input type="text" v-model="linkUrl" class="bg-transparent text-white text-sm flex-grow outline-none" />
    </div>

    <button
      class="bg-white text-[#FF4863] w-full py-2 rounded text-base font-semibold hover:bg-gray-100 transition-colors">
      リンク！
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const linkUrl = ref('https://localhost:3000');
</script>