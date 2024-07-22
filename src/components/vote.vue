<template>
  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 slideDown mr-24" v-if="0 == displayNum">
    <div class="flex items-center mb-4">
      <div class="w-8 h-8 bg-neutral-700 rounded-full mr-3"></div>
      <div class="text-lg flex-grow">
        <input v-model="pollTitle" class="bg-transparent w-full outline-none" placeholder="投票タイトルを入力" />
      </div>
      <div class="flex space-x-2">
        <button class="text-neutral-400 hover:text-neutral-200">
          <i class="fas fa-link"></i>
        </button>
        <button class="text-neutral-400 hover:text-neutral-200">
          <i class="fas fa-image"></i>
        </button>
        <button class="text-neutral-400 hover:text-neutral-200">
          <i class="fas fa-ellipsis-h"></i>
        </button>
      </div>
    </div>

    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-t-lg">
      <div class="space-y-2">
        <div v-for="(option, index) in pollOptions" :key="index" class="flex items-center relative">
          <input v-model="option.text"
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none"
            :placeholder="`選択肢 ${index + 1}`" />
          <button class="absolute right-2"><img src="/images/delete.svg"></button>
        </div>
      </div>

    </div>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-b-lg mb-4">
      <div class="flex items-center ml-2">
        <div class="flex-grow">投稿期間</div>
        <div class="bg-neutral-800 px-3 py-1 rounded">
          {{ pollDuration }} 日
        </div>
      </div>
    </div>

    <div class="flex justify-between items-center">
      <select v-model="selectedInstance" class="bg-neutral-700 text-neutral-200 px-3 py-1 rounded">
        <option disabled value="">インスタンスを選択</option>
        <option v-for="instance in instances" :key="instance" :value="instance">
          {{ instance }}
        </option>
      </select>
      <button @click="handleNext" class="bg-blue-500 text-white px-4 py-1 rounded hover:bg-blue-600">
        ポスト
      </button>
    </div>
  </div>

  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 anim mr-24" v-if="1 == displayNum">
    <div class="flex items-center mb-4">
      <div class="w-8 h-8 bg-neutral-700 rounded-full mr-3"></div>
      <div class="text-lg flex-grow">
        どっち派
      </div>
    </div>

    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-t-lg">
      <div class="space-y-2">
        <div v-for="(option, index) in pollOptions" :key="index" class="flex items-center relative">
          <input v-model="option.text"
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full"
            :placeholder="`選択肢 ${index + 1}`" />
        </div>
      </div>

    </div>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-b-lg">
      <div class="flex items-center ml-2">
        <div class="flex-grow">投稿期間 7/27日まで</div>
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

const query = JSON.parse(sessionStorage.getItem("query"))
console.log(query.link)

if(query.link){
  next()
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