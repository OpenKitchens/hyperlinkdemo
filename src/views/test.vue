<template>
  <div class="bg-violet-700 min-h-screen text-white p-8 wrapper">
    <div class="max-w-2xl mx-auto">
      <!-- Logo -->
      <div class="mb-16 mt-12">
        <h1 class="text-3xl font-bold">
          <img src="/images/logo.svg" width="200">
        </h1>
      </div>

      <!-- Hyperlink Input -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold mb-2">hyperlink</h2>
        <p class="text-sm mb-2">ハイパーリンクで文化を旅する。</p>
        <div class="flex">
          <input
            type="text"
            placeholder="Enter hyperlink"
            class="flex-grow bg-violet-600 text-white px-4 py-2 rounded-l-md focus:outline-none placeholder:text-violet-400"
          />
          <button class="bg-black px-2 py-2 rounded-r-md">
            <img src="/images/arrow-up-right-circle.svg">
          </button>
        </div>
      </div>

      <!-- Trends -->
      <div>
        <h2 class="text-xl mb-4">トレンド</h2>
        <ul>
          <li v-for="trend in trends" :key="trend.id" class="mb-2 flex items-center justify-between">
            <span class="font-semibold">{{ trend.text }}</span>
            <button class="text-purple-300">
              <span class="text-purple-300 text-sm mr-2">{{ trend.chat }}</span>
              <img src="/images/arrow-up-right-circle.svg" class="transform rotate-90 inline-block w-4 opacity-70">
            </button>
          </li>
        </ul>
      </div>
    </div>

    <!-- Footer -->
    <div class="absolute bottom-0 left-0 right-0 p-4 text-purple-400 text-xs">
      <div class="flex flex-wrap justify-center gap-4">
        <img src="/images/twitter.svg"><span>@alterna_sui</span>
        <img src="/images/envelope-at.svg"><span>shadow.wizard.alterna@gmail.com</span>
        <span>水Protocol</span>
        <span>部屋の中革命犯、アナーキー・イン・ザ・1k</span>
        <span>ワールドワイドウェブに恋をした。</span>
        <span>Return Culture</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const trends = ref([
  { id: 1, text: 'Linux 6.10 カーネルが正式リリー...', chat: '20k' },
  { id: 2, text: 'ニコニコ動画緊急避難所', chat: '155k' },
  { id: 3, text: '#大谷翔平', chat: '20k' },
  { id: 4, text: 'ロックマン リメイク版', chat: '2k' },
]);
</script>

<style scoped>
/* Add any additional styles here if needed */
input {
  font-family: monospace !important;
}

.wrapper {
  box-shadow: inset 0px 0px 25rem rgba(0, 0, 0, 0.8);
}
</style>