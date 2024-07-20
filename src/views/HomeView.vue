<script setup>
// Composition APIのロジックをここに追加できます（必要な場合）
import { ref } from "vue"
import Chat from "@/components/chat.vue"
import Vc from "@/components/vc.vue"
import Share from "@/components/share.vue"

const tab = ref(0)

const change = (num) => {
  tab.value = num
}


const UI = {
  chat: Chat,
  vc: Vc,
  share: Share
}

const trends = ref([
  { id: 1, text: 'Linux 6.10 カーネルが正式リリース', chat: '20k', sub: 'moyasi@温泉同好会 Webサイトを共有(Chat・VC)' },
  { id: 2, text: 'ニコニコ動画緊急避難所', chat: '155k', sub: 'moyasi@温泉同好会 Webサイトを共有(Chat・VC)' },
  { id: 3, text: '#大谷翔平', chat: '20k', sub: 'ブラッティーナチーズ@グローバル Webサイトを共有(Chat・VC)' },
  { id: 4, text: 'ロックマン リメイク版', chat: '2k', sub: 'ブラッティーナチーズ@グローバル Webサイトを共有(Chat・VC)' },
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

<template>
  <div class="flex h-screen max-w-[1020px] mx-auto">
    <aside class="w-64">
      <div class="position fixed w-64 p-4">
        <img src="/images/logo.svg" class="px-3 dark:invert">
        <nav>
          <ul class="mt-8">
            <li @click="change(0)" v-show="tab == 0" class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/house-fill.svg" class="invert px-3 w-12"><p class="my-2 dark:font-bold">ホーム</p></p>
            </li>
            <li @click="change(0)" v-show="tab !== 0" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/house-fill.svg" class="px-3 w-12 dark:invert dark:opacity-50"><p class="my-2">ホーム</p></p>
            </li>

            <li @click="change(1)" v-show="tab == 1" class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/hourglass-split.svg" class="invert px-3 w-12"><p class="my-2 dark:font-bold">履歴</p></p>
            </li>
            <li @click="change(1)" v-show="tab !== 1" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/hourglass-split.svg" class="px-3 w-12 dark:invert dark:opacity-50"><p class="my-2">履歴</p></p>
            </li>

            <li @click="change(2)" v-show="tab == 2" class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/at.svg" class="invert px-3 w-12"><p class="my-2 dark:font-bold">アカウント</p></p>
            </li>
            <li @click="change(2)" v-show="tab !== 2" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/at.svg" class="px-3 w-12 dark:invert dark:opacity-50"><p class="my-2">アカウント</p></p>
            </li>

            <li @click="change(3)" v-show="tab == 3" class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/gear-wide-connected.svg" class="invert px-3 w-12"><p class="my-2 dark:font-bold">設定</p></p>
            </li>
            <li @click="change(3)" v-show="tab !== 3" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/gear-wide-connected.svg" class="px-3 w-12 dark:invert dark:opacity-50"><p class="my-2">設定</p></p>
            </li>
          </ul>
        </nav>
      </div>
    </aside>
    <main class="flex-1 flex flex-col">
      <div class="mt-4 h-15 border border-gray-300 rounded-t-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700">
        <div class="flex m-2 input">
          <input type="text" placeholder="Enter hyperlink" v-model="input" @keydown.enter="constract"
            class="flex-grow bg-white border border-gray-300 border-r-0 text-black px-4 py-2 rounded-l-md focus:outline-none placeholder:text-neutral-400 dark:bg-neutral-800 dark:border-neutral-700 dark:text-white" />

          <button class="py-1 px-3 text-base font-semibold transition-colors border-gray-300 border border-x-0 bg-white dark:bg-neutral-800 dark:border-neutral-700"
            @click="input = ''; constract()" v-show="!input == ''">
            <img src="/images/plus-circle-fill.svg" class="w-4 opacity-70 hover:opacity-100 rotate-45 dark:invert">
          </button>

          <button class="bg-black px-2 py-2 rounded-r-md dark:bg-blue-700" @click="constract">
            <img src="/images/arrow-up-right-circle.svg">
          </button>
        </div>
      </div>
      <div class="border border-gray-300 dark:border-neutral-700 border-t-0">
        <div class="m-2 w-full anime slideDown">
          <component :is="currentComponent" :key="componentsKey"></component>
        </div>
      </div>
      <div class="border border-gray-300 bg-neutral-50 dark:border-neutral-700 dark:bg-neutral-900 border-t-0">
        <div class="flex overflow-x-scroll">
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">グローバル</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">ダイレクト</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">トレンド</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">サイト</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">投稿</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">温泉同好会</p>
        </div>
      </div>

      <div class="border border-gray-300 rounded-b-lg mb-24 dark:border-neutral-700 dark:bg-neutral-900 border-t-0">
        <div class="bg-[url('/images/cover.webp')] w-full h-64 relative before:bg-[#0000000A]">
          <div class="absolute inset-x-0 bottom-0 h-1/3 bg-gradient-to-b from-transparent to-black">
            <p class="text-xl font-bold text-white ml-2">【雑談】焼き肉シュミレーターでなんか話そうぜ</p>
            <p class="text-white font-sm ml-2 opacity-80">結局からあげにレモンかける奴がいっちゃんあかん</p>
            <p class="text-white font-sm ml-2 opacity-80">@温泉同好会</p>
          </div>
        </div>

        <ul class="py-4 bg-neutral-50 rounded-b-lg dark:bg-neutral-900">
          <li v-for="trend in trends" :key="trend.id" class="mb-4 px-5">
            <div class="flex items-center justify-between">
              <span class="font-semibold text-black text-lg dark:text-white">{{ trend.text }}</span>
              <button class="text-neutral-300">
                <span class="text-neutral-400 text-sm mr-2">{{ trend.chat }}</span>
                <img src="/images/arrow-up-right-circle.svg"
                  class="invert transform rotate-90 inline-block w-4 opacity-70 dark:invert-0">
              </button>
            </div>
            <p class="text-sm">{{ trend.sub }}</p>
          </li>
        </ul>
      </div>
      <div class="text-[#00000000]">半径0mの世界を変える 革命起こす幕開けの夜</div>
    </main>

    <aside class="w-32">
    </aside>
  </div>

  <div class="position fixed bottom-0 left-0 right-0 p-4 text-neutral-700 dark:text-neutral-500 text-xs bg-white border-t border-neutral-200 dark:bg-neutral-800 dark:border-neutral-700">
    <div class="flex flex-wrap justify-center gap-4">
      <img src="/images/twitter.svg" class="invert dark:invert-0"><span>@alterna_sui</span>
      <img src="/images/envelope-at.svg" class="invert dark:invert-0"><span>shadow.wizard.alterna@gmail.com</span>
      <span>水Protocol</span>
      <span>部屋の中革命犯、アナーキー・イン・ザ・1k</span>
      <span>ワールドワイドウェブに恋をした。</span>
      <span>Return Culture</span>
    </div>
  </div>
</template>

<style scoped>
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