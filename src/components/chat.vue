<template>
  <div class="bg-[#FF5E72] text-white p-5 rounded-lg max-w-sm font-sans slideDown" v-if="0 == displayNum">
    <div class="flex">
      <h2 class="text-lg font-bold mb-2">チャット先を指定</h2>
      <button class="ml-auto"><img src="/images/indent.svg" class="invert w-6"></button>
    </div>
    <p class="text-sm mb-4">チャット先が指定されていません。</p>

    <div class="bg-neutral-800 rounded flex items-center p-2 mb-3">
      <span class="mr-2"><img src="/images/link.svg" class="invert w-6"></span>
      <input type="text" v-model="linkUrl" class="bg-transparent text-white text-sm flex-grow outline-none" />
    </div>

    <button
      class="bg-white text-[#FF5E72] w-full py-2 rounded text-base font-semibold hover:bg-neutral-100 transition-colors"
      @click="next">
      リンク！
    </button>
  </div>

  <div class="bg-neutral-800 border border-neutral-700 text-white p-4 rounded-lg max-w-md font-sans overflow-hidden" v-if="1 == displayNum">
    <div class="anim">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-lg font-bold ml-2">chat #水曜のダウンタウン実況</h2>
        
        <button class="bg-neutral-700 rounded flex">
          <p class="px-1 flex"><img src="/images/person-fill.svg" class="invert">42</p>
          <p class="px-1 flex"><img src="/images/eye-fill.svg" class="invert">127</p>
        </button>

        <button class="text-neutral-400">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>
      <p class="text-sm text-neutral-400 mb-4 ml-2">製作者: すい@0x9C8fF314C9Bc7F6e59A9d9225Fb22946...</p>

      <div class="space-y-4 mb-4 max-h-80 overflow-y-auto">
        <div v-for="(message, index) in messages" :key="index" class="flex items-start space-x-3">
          <img :src="message.avatar" alt="User Avatar" class="w-10 h-10 rounded-full">
          <div>
            <div class="flex items-center space-x-2">
              <span class="font-semibold">{{ message.username }}</span>
              <span class="text-xs text-neutral-400">{{ message.timestamp }}</span>
            </div>
            <p>{{ message.content }}</p>
          </div>
        </div>
      </div>

      <div class="flex items-center bg-neutral-900 border border-neutral-700 rounded-lg p-2">
        <input type="text" placeholder="#水曜のダウンタウン実況へメッセージを送信"
          class="bg-transparent flex-grow text-sm focus:outline-none">
        <button class="text-neutral-400 ml-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
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