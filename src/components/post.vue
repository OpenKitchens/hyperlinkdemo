<template>
  <div class="p-4 rounded-lg bg-neutral-800 border border-neutral-700 mr-4 slideDown" v-if="0 == displayNum">
    <div class="flex mb-4">
      <img src="/images/acheader.png" class="w-8 h-8 rounded-full mr-2">

      <textarea v-model="postContent" class="focus:outline-none w-full bg-neutral-800 text-neutral-200 p-2 rounded mb-4" rows="3"
        placeholder="今何してる？"></textarea>
    </div>
    <div class="flex justify-between items-center">
      <div class="flex space-x-2">
        <button v-for="size in ['small', 'medium', 'large']" :key="size" @click="fontSize = size"
          class="text-neutral-400 hover:text-neutral-200" :class="{ 'text-neutral-200': fontSize === size }">
          A
        </button>
      </div>
      <div class="flex space-x-2">
        <select v-model="selectedInstance" class="bg-neutral-700 text-neutral-200 px-3 py-1 rounded">
          <option disabled value="">インスタンスを選択</option>
          <option v-for="instance in instances" :key="instance" :value="instance">
            {{ instance }}
          </option>
        </select>
        <button @click="next" class="bg-neutral-200 text-black px-4 py-1 rounded hover:bg-neutral-100">
          ポスト
        </button>
      </div>
    </div>
  </div>

  <div class="bg-[#7A55FD] flex flex-col p-6 rounded-lg max-w-md overflow-hidden" v-if="1 == displayNum">
    <div class="anim">
      <div class="flex items-center mb-4">
        <img src="/images/check-circle-fill.svg" class="w-8 mr-2 invert">
        <span class="text-white text-xl font-bold">ポスト済み</span>
      </div>
      <button class="text-white mt-2">
        <span class="text-white text-sm mr-2 opacity-70">ポストを表示する</span>
        <img src="/images/arrow-up-right-circle.svg" class="transform rotate-90 inline-block w-4 opacity-70">
      </button>
      <p class="text-sm mt-2 text-white">引き続き素敵なインターネットライフを！</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const postContent = ref('');
const fontSize = ref('medium');
const selectedInstance = ref('');
const instances = ['インスタンス1', 'インスタンス2', 'インスタンス3'];

const submitPost = () => {
  // Implement post submission logic here
  console.log('Posting:', postContent.value, 'to', selectedInstance.value);
};

const displayNum = ref(0)

const next = () => {
  displayNum.value++
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