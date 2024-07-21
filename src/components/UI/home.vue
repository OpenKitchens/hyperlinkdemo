<template>
  <main class="flex-1 flex flex-col">
    <div class="mt-4 h-15 border border-gray-300 rounded-t-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700">
      <div class="flex m-2 input">
        <input type="text" placeholder="Enter hyperlink" v-model="input" @keydown.enter="constract"
          class="flex-grow bg-white border border-gray-300 border-r-0 text-black px-4 py-2 rounded-l-md focus:outline-none placeholder:text-neutral-400 dark:bg-neutral-800 dark:border-neutral-700 dark:text-white" />

        <button
          class="py-1 px-3 text-base font-semibold transition-colors border-gray-300 border border-x-0 bg-white dark:bg-neutral-800 dark:border-neutral-700"
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
          <p class="text-xl font-bold text-white ml-5">【雑談】焼き肉シュミレーターでなんか話そうぜ</p>
          <p class="text-white font-sm ml-5 opacity-80">結局からあげにレモンかける奴がいっちゃんあかん</p>
          <p class="text-white font-sm ml-5 opacity-80">@温泉同好会</p>
        </div>
      </div>

      <ul class="pt-4 bg-neutral-50 rounded-b-lg dark:bg-neutral-900">
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

        <p class="px-auto w-full bg-neutral-800 py-3 rounded-b-lg pl-5">もっと見る...</p>
      </ul>
    </div>
    <div class="text-[#00000000]">半径0mの世界を変える 革命起こす幕開けの夜</div>
  </main>
</template>