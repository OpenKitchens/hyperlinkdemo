<script setup>
// Composition APIのロジックをここに追加できます（必要な場合）
import { ref } from "vue"
import Chat from "@/components/chat.vue"
import Vc from "@/components/vc.vue"
import Share from "@/components/share.vue"
import Post from "@/components/post.vue"
import Vote from "@/components/vote.vue"
import Dm from "@/components/dm.vue"
import Radio from "@/components/radio.vue"
import createSites from "@/components/createSites.vue"

sessionStorage.setItem('query', JSON.stringify({ link: "https://localhost:3000" }));
</script>

<template>
  <div class="flex h-screen max-w-[1280px] mx-auto">

    <main class="flex-1 flex flex-col h-dvh">
      <iframe src="https://japan.zdnet.com/article/35221489/" class="bg-white m-6 focus:outline-none rounded-lg border-2 border-neutral-700"
        style="height: calc(100% - 3rem);width: calc(100% - 3rem)"></iframe>
    </main>

    <aside class="w-[28rem] h-dvh">
      <div class="mt-6">
        <Chat />
      </div>
      <div class="my-6 fixed bottom-0">
        <Vc class="w-[28rem]" />
      </div>
    </aside>
  </div>
</template>

<style scoped>
.input {
  transition: box-shadow 0.3s ease;
  border-radius: 0.4rem;
}

/* フォーカス時のスタイル */
.input:hover {
  outline: none;
  /* デフォルトのアウトラインを消す */
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.5);
  /* ブルーのシャドウを追加 */
  border-radius: 0.4rem;
}
</style>

<style>
.slideDown {
  transform: scaleY(0);
  transform-origin: top;
  transition: transform 0.26s ease;
  animation: slideDown 0.26s ease forwards;
  /* 遅延時間を調整 */
}

@keyframes slideDown {
  0% {
    transform: scaleY(0);
  }

  100% {
    transform: scaleY(1);
  }
}
</style>