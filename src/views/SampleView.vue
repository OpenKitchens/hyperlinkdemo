<template>
  <div class="bg-gray-900 text-white min-h-screen p-6">
    <h1 class="text-2xl font-bold mb-6">サイトコンストラクタ</h1>
    <div class="flex space-x-6">
      <div class="w-1/2">
        <h2 class="text-xl mb-2">Markdown</h2>
        <textarea
          v-model="markdownContent"
          @input="updatePreview"
          class="w-full h-96 bg-gray-800 text-white p-4 rounded"
        ></textarea>
        <div class="flex items-center mt-4">
          <img :src="userAvatar" alt="User Avatar" class="w-8 h-8 rounded-full mr-2" />
          <span class="mr-2">{{ userName }}</span>
          <span class="text-gray-400">{{ userPlatform }}</span>
        </div>
      </div>
      <div class="w-1/2">
        <h2 class="text-xl mb-2">Preview</h2>
        <div 
          v-html="previewHtml" 
          class="w-full h-96 bg-white text-black p-4 rounded overflow-auto"
        ></div>
      </div>
    </div>
    <div class="flex justify-between mt-6">
      <button
        @click="saveDraft"
        class="bg-gray-700 hover:bg-gray-600 text-white font-bold py-2 px-4 rounded"
      >
        一次保存
      </button>
      <button
        @click="createSite"
        class="bg-green-600 hover:bg-green-500 text-white font-bold py-2 px-4 rounded"
      >
        Create
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { marked } from 'marked'

const markdownContent = ref(`# 友人の万引きと母の思い出

!account

ちいかわのシーサーが「ユニオンですから」と歌うことがある。これは『ユニオン』なる沖縄の地元スーパーのCMソングです。これを聴くと二つのなんともいえない記憶が蘇る。
一つはちょっと明るい記憶。
母親が再婚したことを機に義父と喧嘩し、一週間ほど家出高校生として夜の沖縄を彷徨った。その際、24時間営業がウリのユニオンは夜風を凌ぐ休憩所としてお世話になったし、店員からデカいダンボールをもらい、それをベッドや掛け布団にして公園で眠っていた。ユニオンに関する暖かな思い出。
二つ目はなんとも言えない出来事です。
中学の頃、友人と二人でユニオンに入店し、適当にぶらついて店を出たところ、友人が万引き6メンちらし男に捕まった。

taila://api.radio`)

const previewHtml = computed(() => marked(markdownContent.value))

const userName = ref('Alterna gen...')
const userPlatform = ref('Github')
const userAvatar = ref('/api/placeholder/32/32') // プレースホルダー画像を使用

const updatePreview = () => {
  // プレビューは自動的に更新されるため、追加のロジックは不要
}

const saveDraft = () => {
  console.log('Draft saved')
  // ここに下書き保存のロジックを実装
}

const createSite = () => {
  console.log('Site created')
  // ここにサイト作成のロジックを実装
}
</script>