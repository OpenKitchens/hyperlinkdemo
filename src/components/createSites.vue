<template>
  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 slideDown mr-24"
    v-if="0 == displayNum">
    <h2 class="font-bold text-lg">サイトコンストラクタ</h2>

    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-lg mt-5">
      <div class="space-y-2">
        <div class="flex items-center relative">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none"
            placeholder="Domain" />
          <button class="absolute right-2"><img src="/images/add.svg" class="w-6"></button>
        </div>
        <div class="flex items-center relative">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none"
            placeholder="Deploy" />
          <button class="absolute right-2"><img src="/images/chevron-down.svg" class="w-6 invert"></button>
        </div>
      </div>
    </div>

    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-lg my-5">
      <h2 class="text-lg font-bold mb-2 flex">theme</h2>
      <h2 class="text-sm mb-4 opacity-80">テーマを変更しますか？</h2>
      <div class="flex">
        <img src="/images/Ellipse.png" class="w-20 h-20">
        <div class="my-auto ml-5">
          <h2 class="text-lg font-bold flex">Alterna general theme<img src="/images/arrow-up-right-circle.svg"
            class="ml-2 w-5"></h2>
          <p>github @alternadenki</p>
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
        コンストラクト！
      </button>
    </div>
  </div>

  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 anim mr-24" v-if="1 == displayNum">
    エディットに転送...
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';
import { useRouter } from 'vue-router'
const router = useRouter()


const emit = defineEmits(['next']);

const handleNext = () => {
  next();
  console.log("next"); // 確認用ログ
  emit('next');
  router.push("edit")
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