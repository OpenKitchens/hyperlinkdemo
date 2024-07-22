<template>
  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 slideDown mr-4"
    v-if="0 == displayNum">
    <h2 class="text-lg font-bold mb-4">ラジオアップロード</h2>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-t-lg">
      <div class="space-y-2">
        <div class="flex items-center relative">
          <input
            class="bg-neutral-800 text-neutral-200 p-2 rounded-lg flex-grow border border-neutral-600 w-full focus:outline-none"
            placeholder="タイトル" />
          <button class="absolute right-2"><img src="/images/delete.svg"></button>
        </div>

        <div class="bg-neutral-700 border border-neutral-600 flex p-5 rounded-lg">
          <img src="/images/cloud-upload-fill.svg" class="invert w-10">
          <h2 class="text-lg font-bold mb-4 m-4">Upload</h2>
        </div>
      </div>

    </div>
    <div class="bg-[#333333] border border-neutral-600 p-3 rounded-b-lg mb-4">
      <div class="flex items-center ml-2">
        <h2 class="text-lg font-bold">Add content</h2>
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

  <div class="text-neutral-200 p-4 rounded-lg bg-[#262626] border border-neutral-700 anim flex"
    v-if="1 == displayNum">
    <div class="mr-5">
      <img src="/images/cover.png" class="w-60 rounded">
      <h2 class="text-lg font-bold mt-3">Up Night Radio</h2>
      <p>私は多年とう拡張家</p>
    </div>
    <div class="w-full">
      <div class="bg-[#333333] border border-neutral-600 p-3 rounded-t-lg w-full">
        <div class="space-y-2">
          <div class="flex items-center relative">
            <img src="/images/play.svg" class="invert w-6 mr-5">
            <h2 class="font-bold">#0 テスト音源</h2>
          </div>
        </div>
      </div>
      <div class="bg-[#333333] border border-neutral-600 p-3 w-full">
        <div class="space-y-2">
          <div class="flex items-center relative">
            <img src="/images/play.svg" class="invert w-6 mr-5">
            <h2 class="font-bold">#1 テスト音源</h2>
          </div>
        </div>
      </div>
      <div class="bg-[#333333] border border-neutral-600 p-3 w-full">
        <div class="space-y-2">
          <div class="flex items-center relative">
            <img src="/images/play.svg" class="invert w-6 mr-5">
            <h2 class="font-bold">#2 テスト音源</h2>
          </div>
        </div>
      </div>
      <div class="bg-[#333333] border border-neutral-600 p-3 w-full">
        <div class="space-y-2">
          <div class="flex items-center relative">
            <img src="/images/play.svg" class="invert w-6 mr-5">
            <h2 class="font-bold">#3 テスト音源</h2>
          </div>
        </div>
      </div>
      <div class="bg-[#333333] border border-neutral-600 p-3 w-full rounded-b-lg">
        <div class="space-y-2">
          <div class="flex items-center relative">
            <img src="/images/play.svg" class="invert w-6 mr-5">
            <h2 class="font-bold">#3 テスト音源</h2>
          </div>
        </div>
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

const query = JSON.parse(sessionStorage.getItem("query"));
console.log(query.link);

if(query.link){
  next();
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

const displayNum = ref(0);

const next = () => {
  displayNum.value++;
};
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