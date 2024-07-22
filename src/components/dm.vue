<template>
  <div class="bg-[#262626] border border-neutral-700 text-neutral-200 p-4 rounded-lg mr-4 slideDown" v-if="0 == displayNum">

    <div class="mb-4 text-lg font-bold">メッセージ</div>

    <div class="mb-4 flex hover:bg-neutral-700 p-2 rounded" @click="handleNext">
      <img src="/images/acheader.png" class="w-12 h-12 rounded-full mr-2">
      <div>
        <p class="text-lg">窪@alterna</p>
        <p class="text-sm">先日は、お返事いただきありがとうござい...</p>
      </div>
    </div>
    <div class="mb-4 flex hover:bg-neutral-700 p-2 rounded" @click="handleNext">
      <img src="/images/acheader.png" class="w-12 h-12 rounded-full mr-2">
      <div>
        <p class="text-lg">窪@alterna</p>
        <p class="text-sm">先日は、お返事いただきありがとうござい...</p>
      </div>
    </div>
    <div class="mb-4 flex hover:bg-neutral-700 p-2 rounded" @click="handleNext">
      <img src="/images/acheader.png" class="w-12 h-12 rounded-full mr-2">
      <div>
        <p class="text-lg">窪@alterna</p>
        <p class="text-sm">先日は、お返事いただきありがとうござい...</p>
      </div>
    </div>
  </div>

  <div class="bg-[#262626] border border-neutral-700 text-neutral-200 p-4 rounded-lg mr-4 anim" v-if="1 == displayNum">
    <div class="mb-4 text-lg">窪@alterna</div>

    <div class="space-y-4 mb-4">
      <div class="flex justify-end">
        <div class="bg-purple-600 text-white px-4 py-2 rounded-full">
          テストテキスト
        </div>
      </div>

      <div class="flex">
        <div class="w-8 h-8 bg-neutral-700 rounded-full mr-3"></div>
        <div class="bg-neutral-700 text-white px-4 py-2 rounded-2xl">
          イーハトーヴォの風の音所業
        </div>
      </div>

      <div class="flex justify-end">
        <div class="bg-purple-600 text-white px-4 py-2 rounded-full">
          テストテキスト
        </div>
      </div>
    </div>

    <div class="relative">
      <input v-model="message"
        class="w-full bg-[#333333] border border-neutral-600 text-neutral-200 p-3 pr-24 rounded-lg focus:outline-none"
        placeholder="ここに入力" />
      <div class="absolute right-2 top-1/2 transform -translate-y-1/2 flex space-x-2">
        <button v-for="size in ['small', 'medium', 'large']" :key="size" @click="fontSize = size"
          class="text-neutral-400 hover:text-neutral-200" :class="{ 'text-neutral-200': fontSize === size }">
          A
        </button>
      </div>
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

const pollTitle = ref('');
const pollOptions = ref([
  { text: 'イヌ派' },
  { text: 'ネコ派' }
]);
const pollDuration = ref(7);
const selectedInstance = ref('');
const instances = ['インスタンス1', 'インスタンス2', 'インスタンス3'];

const submitPoll = () => {
  console.log('Posting poll:', {
    title: pollTitle.value,
    options: pollOptions.value,
    duration: pollDuration.value,
    instance: selectedInstance.value
  });
};

const displayNum = ref(0)

const next = () => {
  displayNum.value++
}
</script>

<style scoped>
/* Add any additional styles here */
</style>


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