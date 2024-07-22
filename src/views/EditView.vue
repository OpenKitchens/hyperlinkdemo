<template>
  <div class="bg-neutral-900 text-white min-h-screen p-6">
    <h1 class="text-2xl font-bold mb-6">サイトコンストラクタ</h1>
    <div class="flex space-x-6">
      <div class="w-1/2">
        <h2 class="text-xl mb-2">Markdown</h2>
        <div class="bg-[#333333] border border-neutral-600 p-3 rounded-lg my-5">
          <textarea v-model="markdownContent" @input="updatePreview"
            class="w-full h-[29rem] bg-neutral-800 text-white p-4 rounded focus:outline-none" @keydown.enter="constract"></textarea>
        </div>
        <component :is="currentComponent" :key="componentsKey" @next="next"></component>

      </div>
      <div class="w-1/2">
        <h2 class="text-xl mb-4">Preview</h2>
        <img src="/images/preview.png" class="rounded">
        <div class="flex bg-[#333333] border border-neutral-600 p-3 rounded-lg mt-4">
          <button @click="saveDraft" class="bg-neutral-700 hover:bg-neutral-600 text-white font-bold py-2 px-4 rounded w-2/3">
            一次保存
          </button>
          <button @click="createSite" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded w-1/3 ml-4">
            Create
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const markdownContent = ref(`# 友人の万引きと母の思い出

!account

ちいかわのシーサーが「ユニオンですから」と歌うことがある。これは『ユニオン』なる沖縄の地元スーパーのCMソングです。これを聴くと二つのなんともいえない記憶が蘇る。
一つはちょっと明るい記憶。
母親が再婚したことを機に義父と喧嘩し、一週間ほど家出高校生として夜の沖縄を彷徨った。その際、24時間営業がウリのユニオンは夜風を凌ぐ休憩所としてお世話になったし、店員からデカいダンボールをもらい、それをベッドや掛け布団にして公園で眠っていた。ユニオンに関する暖かな思い出。
二つ目はなんとも言えない出来事です。
中学の頃、友人と二人でユニオンに入店し、適当にぶらついて店を出たところ、友人が万引き6メンちらし男に捕まった。

taila://api.radio`)

const extractApiComponent = (text) => {
    // 正規表現でtaila://で始まり、api.の後ろの部分を抽出する
    const regex = /taila:\/\/api\.([^\s]+)/;
    const match = text.match(regex);

    if (match && match[1]) {
        return match[1];
    } else {
        return null;
    }
}

import Chat from "@/components/chat.vue"
import Vc from "@/components/vc.vue"
import Share from "@/components/share.vue"
import Post from "@/components/post.vue"
import Vote from "@/components/vote.vue"
import Dm from "@/components/dm.vue"
import Radio from "@/components/radio.vue"
import createSites from "@/components/createSites.vue"

const UI = {
  chat: Chat,
  vc: Vc,
  share: Share,
  post: Post,
  vote: Vote,
  dm: Dm,
  radio: Radio,
  createsites: createSites
}

const currentComponent = ref();
const componentsKey = ref(0)

const constract = () => {
  currentComponent.value = false

  const url = markdownContent.value;
  const regex = /(?<=:\/\/api\.)\w+/;
  const match = url.match(regex);

  if (match) {
    currentComponent.value = UI[match[0]]
    componentsKey.value++
  }
}

const next = () => {
  const url = markdownContent.value;
  const regex = /(?<=:\/\/api\.)\w+/;
  const match = url.match(regex);

  markdownContent.value = markdownContent.value.replace('taila://api.'+match[0], 'taila://api.'+match[0]+'?link=https://example.com')
  console.log("next")
}
</script>