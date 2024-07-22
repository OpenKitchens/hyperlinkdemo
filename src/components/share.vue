<template>

  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 slideDown mr-4"
    v-if="0 == displayNum">
    <h2 class="text-lg font-bold mb-4">スーパーシェア先を指定</h2>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-lg">
      <div class="">
        <div class="flex items-center relative mb-2">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none pl-10"
            placeholder="localhost:3000" />
          <button class="absolute left-2"><img src="/images/link.svg" class="invert w-6"></button>
        </div>
        <div class="flex items-center relative mb-6">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none pl-10"
            placeholder="@everyone" />
          <button class="absolute left-2"><img src="/images/person-fill.svg" class="invert w-6"></button>
        </div>
        <div class="flex items-center relative mb-2">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none pl-10"
            placeholder="taila://api.chat" />
          <button class="absolute left-2"><img src="/images/bezier.svg" class="invert w-6"></button>
        </div>
        <div class="flex items-center relative mb-2">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none pl-10"
            placeholder="taila://api.vc" />
          <button class="absolute left-2"><img src="/images/bezier.svg" class="invert w-6"></button>
        </div>
        <div class="flex items-center relative mb-2">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none pl-10"
            placeholder="taila://api.readme" />
          <button class="absolute left-2"><img src="/images/bezier.svg" class="invert w-6"></button>
        </div>
      </div>
    </div>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-lg my-5">
      <h2 class="text-lg font-bold mb-2 flex">Basic Theme<img src="/images/arrow-up-right-circle.svg" class="ml-2 w-5"></h2>
      <h2 class="text-sm mb-4 opacity-80">テーマを変更しますか？</h2>
      <img src="/images/basic_theme.png">
    </div>

    <div class="flex justify-between items-center">
      <select v-model="selectedInstance" class="bg-neutral-700 text-neutral-200 px-3 py-1 rounded">
        <option disabled value="">インスタンスを選択</option>
        <option v-for="instance in instances" :key="instance" :value="instance">
          {{ instance }}
        </option>
      </select>
      <button @click="handleNext" class="bg-blue-500 text-white px-4 py-1 rounded hover:bg-blue-600">
        リンク!
      </button>
    </div>
  </div>

  <div class="bg-[#7A55FD] flex flex-col p-6 rounded-lg max-w-md overflow-hidden" v-if="1 == displayNum">
    <div class="anim">
      <div class="flex items-center mb-4">
        <img src="/images/check-circle-fill.svg" class="w-8 mr-2 invert">
        <span class="text-white text-xl font-bold">シェアしました！</span>
      </div>
      <button class="text-white mt-2">
        <span class="text-white text-sm mr-2 opacity-70">shareインスタンスで待機する</span>
        <img src="/images/arrow-up-right-circle.svg" class="transform rotate-90 inline-block w-4 opacity-70">
      </button>
      <p class="text-sm mt-2 text-white">引き続き素敵なインターネットライフを！</p>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits(['next']);

const handleNext = () => {
  next();
  console.log("next"); // 確認用ログ
  emit('next');
};


const query = JSON.parse(sessionStorage.getItem("query"))
console.log(query.link)

if(query.link){
  next()
}

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


const postContent = ref('');
const fontSize = ref('medium');
const selectedInstance = ref('');
const instances = ['インスタンス1', 'インスタンス2', 'インスタンス3'];

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