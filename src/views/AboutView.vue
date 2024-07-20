
<template>
  <div class="bg-zinc-100 min-h-screen h-full text-white p-8">
    <div class="max-w-2xl mx-auto">
      <!-- Logo -->
      <div class="mb-16 mt-12">
        <h1 class="text-3xl font-bold">
          <img src="/images/logo.svg" width="200" class="invert">
        </h1>
      </div>

      <!-- Hyperlink Input -->
      <div class="mb-8">
        <h2 class="text-xl font-semibold mb-2 text-black">hyperlink</h2>
        <p class="text-sm mb-2 text-zinc-400">ハイパーリンクで文化を旅する。</p>
        <div class="flex input">
          <input type="text" placeholder="Enter hyperlink" v-model="input" @keydown.enter="constract"
            class="flex-grow bg-white border border-r-0 text-black px-4 py-2 rounded-l-md focus:outline-none placeholder:text-zinc-400" />

          <button class="py-1 px-3 text-base font-semibold transition-colors border border-x-0 bg-white"
            @click="input = ''; constract()" v-show="!input == ''">
            <img src="/images/plus-circle-fill.svg" class="w-4 opacity-70 hover:opacity-100 rotate-45">
          </button>

          <button class="bg-black px-2 py-2 rounded-r-md" @click="constract">
            <img src="/images/arrow-up-right-circle.svg">
          </button>
        </div>

        <div class="mt-2 w-full anime">
          <component :is="currentComponent" :key="componentsKey"></component>
        </div>
      </div>

      <div>
        <h2 class="text-xl mb-4 text-black">ダイレクトシェア</h2>
        <ul class="mb-4">
          <li v-for="trend in trends" :key="trend.id" class="mb-2 flex items-center justify-between">
            <span class="font-semibold text-black">{{ trend.text }}</span>
            <button class="text-zinc-300">
              <span class="text-zinc-400 text-sm mr-2">{{ trend.chat }}</span>
              <img src="/images/arrow-up-right-circle.svg"
                class="invert transform rotate-90 inline-block w-4 opacity-70">
            </button>
          </li>
        </ul>
        <span class="text-zinc-400 flex"><img src="/images/arrow-return-right.svg" class="opacity-40 mr-1">もっとみる</span>
      </div>
      
      <div>
        <h2 class="text-xl mb-4 text-black">インスタンス内</h2>
        <ul class="mb-4">
          <li v-for="trend in trends" :key="trend.id" class="mb-2 flex items-center justify-between">
            <span class="font-semibold text-black">{{ trend.text }}</span>
            <button class="text-zinc-300">
              <span class="text-zinc-400 text-sm mr-2">{{ trend.chat }}</span>
              <img src="/images/arrow-up-right-circle.svg"
                class="invert transform rotate-90 inline-block w-4 opacity-70">
            </button>
          </li>
        </ul>
        <span class="text-zinc-400 flex"><img src="/images/arrow-return-right.svg" class="opacity-40 mr-1">もっとみる</span>
      </div>

      <!-- Trends -->
      <div>
        <h2 class="text-xl mb-4 text-black mt-8">トレンド</h2>
        <ul class="mb-4">
          <li v-for="trend in trends" :key="trend.id" class="mb-2 flex items-center justify-between">
            <span class="font-semibold text-black">{{ trend.text }}</span>
            <button class="text-zinc-300">
              <span class="text-zinc-400 text-sm mr-2">{{ trend.chat }}</span>
              <img src="/images/arrow-up-right-circle.svg"
                class="invert transform rotate-90 inline-block w-4 opacity-70">
            </button>
          </li>
        </ul>
        <span class="text-zinc-400 flex"><img src="/images/arrow-return-right.svg" class="opacity-40 mr-1">もっとみる</span>
      </div>

      <div class="mb-24">
        <h2 class="text-xl mb-4 text-black mt-8">履歴</h2>
        <ul class="mb-4">
          <li v-for="trend in trends" :key="trend.id" class="mb-2 flex items-center justify-between">
            <span class="font-semibold text-black">{{ trend.text }}</span>
          </li>
        </ul>
        <span class="text-zinc-400 flex"><img src="/images/arrow-return-right.svg" class="opacity-40 mr-1">もっとみる</span>
      </div>
    </div>

    <!-- Footer -->
    <div class="position fixed bottom-0 left-0 right-0 p-4 text-zinc-700 text-xs bg-white border-t border-zinc-200">
      <div class="flex flex-wrap justify-center gap-4">
        <img src="/images/twitter.svg" class="invert"><span>@alterna_sui</span>
        <img src="/images/envelope-at.svg" class="invert"><span>shadow.wizard.alterna@gmail.com</span>
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
import Chat from "@/components/chat.vue"
import Vc from "@/components/vc.vue"
import Share from "@/components/share.vue"

const UI = {
  chat: Chat,
  vc: Vc,
  share: Share
}

const trends = ref([
  { id: 1, text: 'Linux 6.10 カーネルが正式リリー...', chat: '20k' },
  { id: 2, text: 'ニコニコ動画緊急避難所', chat: '155k' },
  { id: 3, text: '#大谷翔平', chat: '20k' },
  { id: 4, text: 'ロックマン リメイク版', chat: '2k' },
]);

const input = ref()

const currentComponent = ref();
const componentsKey = ref(0)

const constract = () => {
  currentComponent.value = false

  const url = input.value;
  const regex = /(?<=:\/\/api\.)\w+/;
  const match = url.match(regex);
  const queryParams = getQueryParams(url)

  sessionStorage.setItem('query', JSON.stringify(queryParams));

  if (match) {
    currentComponent.value = UI[match[0]]
    componentsKey.value++
  }
}



function getQueryParams(url) {
  const params = new URLSearchParams(new URL(url).search);
  const queryParams = {};

  params.forEach((value, key) => {
    queryParams[key] = value;
  });

  return queryParams;
}
</script>

<style scoped>
/* Add any additional styles here if needed */
input {
  font-family: monospace !important;
}

.wrapper {
  box-shadow: inset 0px 0px 25rem rgba(0, 0, 0, 0.8);
}

.input {
  transition: box-shadow 0.3s ease;
  border-radius: 0.4rem;
}

/* フォーカス時のスタイル */
.input:hover {
  outline: none;
  /* デフォルトのアウトラインを消す */
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.5);
  /* ブルーのシャドウを追加 */
  border-radius: 0.4rem;
}
</style>

<style>
.slideDown {
  transform: scaleY(0);
  transform-origin: top;
  transition: transform 0.26s ease;
  animation: slideDown 0.26s ease forwards;
  /* 遅延時間を調整 */
}

@keyframes slideDown {
  0% {
    transform: scaleY(0);
  }

  100% {
    transform: scaleY(1);
  }
}
</style>