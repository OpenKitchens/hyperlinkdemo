<template>
  <div class="bg-[#7A55FD] text-white p-5 rounded-lg max-w-sm font-sans slideDown"
    v-if="0 == displayNum">
    <div class="flex">
      <h2 class="text-lg font-bold mb-2">ボイスチャット先を指定</h2>
      <button class="ml-auto"><img src="/images/indent.svg" class="invert w-6"></button>
    </div>
    <p class="text-sm mb-4">チャット先が指定されていません。</p>

    <div class="bg-gray-800 rounded flex items-center p-2 mb-3">
      <span class="mr-2"><img src="/images/link.svg" class="invert w-6"></span>
      <input type="text" v-model="linkUrl" class="bg-transparent text-white text-sm flex-grow outline-none" />
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
        <img src="/images/mic-fill.svg" class="w-8 mr-2 invert">
        <span class="text-white text-xl font-bold">ボイスライブ</span>
      </div>
      <div class="flex space-x-2 mb-4">
        <div v-for="participant in participants" :key="participant.id"
          class="bg-[#A68CFF] rounded px-3 py-1 flex items-center">
          <span class="mr-1 py-1"><img :src="'images/'+participant.emoji+'.png'" class="w-6"></span>
          <span class="text-white">{{ participant.count }}b</span>
        </div>
      </div>
      <div class="flex w-full space-x-2">
        <button class="flex-1 bg-white text-[#A68CFF] py-2 px-4 rounded font-bold">
          パーソナリティとして参加
        </button>
        <button class="bg-black text-white py-2 px-8 rounded font-bold">
          参加
        </button>
      </div>
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


const query = JSON.parse(sessionStorage.getItem("query"))
console.log(query.link)

if(query.link){
  next()
}
</script>

<style scoped>
.anim {
  animation: animation 0.5s
}

@keyframes animation {
  0% {
    transform: translateX(50px);
    opacity: 0;
  }

  100% {
    transform: translateX(0px);
    opacity: 1;
  }
}
</style>