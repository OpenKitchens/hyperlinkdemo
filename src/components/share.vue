<template>
  <div class="bg-[#7A55FD] text-white p-5 rounded-lg max-w-sm font-sans slideDown" v-if="0 == displayNum">
    <div class="flex">
      <h2 class="text-lg font-bold mb-2">スーパーシェア先を指定</h2>
      <button class="ml-auto"><img src="/images/indent.svg" class="invert w-6"></button>
    </div>
    <p class="text-sm mb-4">スーパーシェアの対象を見つけられませんでした。</p>

    <div class="bg-gray-800 rounded flex items-center p-2 mb-3">
      <span class="mr-2"><img src="/images/link.svg" class="invert w-6"></span>
      <input type="text" v-model="linkUrl" class="bg-transparent text-white text-sm flex-grow outline-none" />
    </div>

    <p class="text-sm mb-4">共有先</p>

    <div>
      <div class="bg-gray-800 rounded flex items-center p-2 mb-3">
        <span class="mr-2"><img src="/images/person-fill.svg" class="invert w-6"></span>
        <input type="text" class="bg-transparent text-white text-sm flex-grow outline-none" placeholder="@everyone" />

        <button class="py-1 px-1 rounded text-base font-semibold transition-colors" @click="next">
          <img src="/images/plus-circle-fill.svg" class="w-4 invert opacity-70 hover:opacity-100">
        </button>
      </div>
    </div>

    <button
      class="bg-white text-[#7A55FD] w-full py-2 rounded text-base font-semibold hover:bg-gray-100 transition-colors"
      @click="next">
      リンク！
    </button>
  </div>

  <div class="bg-[#7A55FD] flex flex-col p-6 rounded-lg max-w-md overflow-hidden" v-if="1 == displayNum">
    <div class="anim">
      <div class="flex items-center mb-4">
        <img src="/images/check-circle-fill.svg" class="w-8 mr-2 invert">
        <span class="text-white text-xl font-bold">シェアしました！</span>
      </div>
      <p class="text-sm">引き続き素敵なインターネットライフを！</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const linkUrl = ref('https://localhost:3000');

const messages = ref([
  {
    avatar: 'https://via.placeholder.com/40',
    username: 'moyasi@0x9C8fF314C9Bc7F6e59A9d9225Fb22946',
    timestamp: '2024/06/13 21:07',
    content: 'いや草'
  },
  // 同じメッセージを5回繰り返す
  ...Array(5).fill({
    avatar: 'https://via.placeholder.com/40',
    username: 'moyasi@0x9C8fF314C9Bc7F6e59A9d9225Fb22946',
    timestamp: '2024/06/13 21:07',
    content: 'いや草'
  })
]);

const displayNum = ref(0)

const next = () => {
  displayNum.value++
}

const participants = ref([
  { id: 1, emoji: 'smile', count: 12 },
  { id: 2, emoji: 'umm', count: 12 },
  { id: 3, emoji: 'umm', count: 12 },
  { id: 4, emoji: 'smile', count: 12 },
])
</script>

<style scoped>
.anim {
  animation: animation 1s
}

@keyframes animation {
  0% {
    transform: translateX(80px);
    opacity: 0;
  }

  100% {
    transform: translateX(0px);
    opacity: 1;
  }
}
</style>