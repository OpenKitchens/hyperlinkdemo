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

const tab = ref(0)

const change = (num) => {
  tab.value = num
}

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

const trends = ref([
  { id: 1, text: 'Linux 6.10 カーネルが正式リリース', chat: '20k', sub: 'moyasi@温泉同好会 Webサイトを共有(Chat・VC)' },
  { id: 2, text: 'ニコニコ動画緊急避難所', chat: '155k', sub: 'moyasi@温泉同好会 Webサイトを共有(Chat・VC)' },
  { id: 3, text: '#大谷翔平', chat: '20k', sub: 'ブラッティーナチーズ@グローバル Webサイトを共有(Chat・VC)' },
  { id: 4, text: 'ロックマン リメイク版', chat: '2k', sub: 'ブラッティーナチーズ@グローバル Webサイトを共有(Chat・VC)' },
]);

const trans = ref([
  { id: 1, text: 'Smartphone8 inへウォレットを送信', chat: '6時間前', sub: 'ポート 2087・リクエスト9006' },
  { id: 2, text: '産駒@netからサイトへの招待', chat: '6時間前', sub: 'ポート 2087・リクエスト9006' },
  { id: 3, text: 'サイトリンクをBroadcast', chat: '7時間前', sub: 'ポート 2087・リクエスト9006' },
  { id: 4, text: 'サングリアから温泉同好会への参加', chat: '9時間前', sub: 'ポート 2087・リクエスト9006' },
])

const communitys = ref([
  { id: 1, text: '温泉同好会', sub: '310人が参加' },
  { id: 2, text: 'サウナイキタイ', sub: '220人が参加' },
  { id: 2, text: 'なんでも雑談こたつ', sub: '470人が参加' }
])

const input = ref()

const currentComponent = ref();
const componentsKey = ref(0)

const constract = () => {
  currentComponent.value = false

  const url = input.value;
  const regex = /(?<=:\/\/api\.)\w+/;
  const match = url.match(regex);
  const queryParams = getQueryParams(url)

  sessionStorage.setItem('query', JSON.stringify(queryParams));

  if (match) {
    currentComponent.value = UI[match[0]]
    componentsKey.value++
  }
}



function getQueryParams(url) {
  const params = new URLSearchParams(new URL(url).search);
  const queryParams = {};

  params.forEach((value, key) => {
    queryParams[key] = value;
  });

  return queryParams;
}
</script>

<template>
  <div class="flex h-screen max-w-[1280px] mx-auto">
    <aside class="w-72">
      <div class="position fixed w-72 p-4">
        <img src="/images/logo.svg" class="px-3 dark:invert">
        <nav>
          <ul class="mt-8">
            <li @click="change(0)" v-show="tab == 0"
              class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/house-fill.svg" class="invert px-3 w-12">
              <p class="my-2 dark:font-bold">ホーム</p>
              </p>
            </li>
            <li @click="change(0)" v-show="tab !== 0" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/house-fill.svg"
                  class="px-3 w-12 dark:invert dark:opacity-50">
              <p class="my-2">ホーム</p>
              </p>
            </li>

            <li @click="change(1)" v-show="tab == 1"
              class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/hourglass-split.svg" class="invert px-3 w-12">
              <p class="my-2 dark:font-bold">履歴</p>
              </p>
            </li>
            <li @click="change(1)" v-show="tab !== 1" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/hourglass-split.svg"
                  class="px-3 w-12 dark:invert dark:opacity-50">
              <p class="my-2">履歴</p>
              </p>
            </li>

            <li @click="change(2)" v-show="tab == 2"
              class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/at.svg" class="invert px-3 w-12">
              <p class="my-2 dark:font-bold">アカウント</p>
              </p>
            </li>
            <li @click="change(2)" v-show="tab !== 2" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/at.svg" class="px-3 w-12 dark:invert dark:opacity-50">
              <p class="my-2">アカウント</p>
              </p>
            </li>

            <li @click="change(3)" v-show="tab == 3"
              class="bg-black text-white rounded-md dark:bg-[#00000000] dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/gear-wide-connected.svg" class="invert px-3 w-12">
              <p class="my-2 dark:font-bold">設定</p>
              </p>
            </li>
            <li @click="change(3)" v-show="tab !== 3" class="hover:bg-neutral-200 rounded-md dark:hover:bg-neutral-800">
              <p class="mb-3 text-lg flex"><img src="/images/gear-wide-connected.svg"
                  class="px-3 w-12 dark:invert dark:opacity-50">
              <p class="my-2">設定</p>
              </p>
            </li>
          </ul>
        </nav>
      </div>
    </aside>

    <main class="flex-1 flex flex-col" v-show="tab == 0">
      <div class="mt-4 h-15 border border-gray-300 rounded-t-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700">
        <div class="flex m-2 input">
          <input type="text" placeholder="Enter hyperlink" v-model="input" @keydown.enter="constract"
            class="flex-grow bg-white border border-gray-300 border-r-0 text-black px-4 py-2 rounded-l-md focus:outline-none placeholder:text-neutral-400 dark:bg-neutral-800 dark:border-neutral-700 dark:text-white" />

          <button
            class="py-1 px-3 text-base font-semibold transition-colors border-gray-300 border border-x-0 bg-white dark:bg-neutral-800 dark:border-neutral-700"
            @click="input = ''; constract()" v-show="!input == ''">
            <img src="/images/plus-circle-fill.svg" class="w-4 opacity-70 hover:opacity-100 rotate-45 dark:invert">
          </button>

          <button class="bg-black px-2 py-2 rounded-r-md dark:bg-blue-500" @click="constract">
            <img src="/images/arrow-up-right-circle.svg">
          </button>
        </div>
      </div>
      <div class="border border-gray-300 dark:border-neutral-700 border-t-0">
        <div class="m-2 w-full anime slideDown">
          <component :is="currentComponent" :key="componentsKey"></component>
        </div>
      </div>
      <div class="border border-gray-300 bg-neutral-50 dark:border-neutral-700 dark:bg-neutral-900 border-t-0">
        <div class="flex overflow-x-scroll">
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">グローバル</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">ダイレクト</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">トレンド</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">サイト</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">投稿</p>
          <p class="px-4 py-2 hover:bg-neutral-200 font-medium dark:hover:bg-neutral-800">温泉同好会</p>
        </div>
      </div>

      <div class="border border-gray-300 rounded-b-lg mb-6 dark:border-neutral-700 dark:bg-neutral-900 border-t-0">
        <div class="bg-[url('/images/cover.webp')] w-full h-64 relative before:bg-[#0000000A]">
          <div class="absolute inset-x-0 bottom-0 h-1/3 bg-gradient-to-b from-transparent to-black">
            <p class="text-xl font-bold text-white ml-5">【雑談】焼き肉シュミレーターでなんか話そうぜ</p>
            <p class="text-white font-sm ml-5 opacity-80">結局からあげにレモンかける奴がいっちゃんあかん</p>
            <p class="text-white font-sm ml-5 opacity-80">@温泉同好会</p>
          </div>
        </div>

        <ul class="pt-4 bg-neutral-50 rounded-b-lg dark:bg-neutral-900">
          <li v-for="trend in trends" :key="trend.id" class="mb-4 px-5">
            <div class="flex items-center justify-between">
              <span class="font-semibold text-black text-lg dark:text-white">{{ trend.text }}</span>
              <button class="text-neutral-300">
                <span class="text-neutral-400 text-sm mr-2">{{ trend.chat }}</span>
                <img src="/images/arrow-up-right-circle.svg"
                  class="invert transform rotate-90 inline-block w-4 opacity-70 dark:invert-0">
              </button>
            </div>
            <p class="text-sm">{{ trend.sub }}</p>
          </li>

          <p class="px-auto w-full bg-neutral-200 dark:bg-neutral-800 py-3 rounded-b-lg pl-5">もっと見る...</p>
        </ul>
      </div>

      <div
        class="mt-4 h-15 border border-gray-300 rounded-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700 mb-24">
        <p class="text-lg font-bold dark:text-white ml-5 my-3">シーズン</p>
        <div class="dark:bg-neutral-900 rounded-b-lg">
          <div
            class="bg-[url('/images/background.png')] w-full h-32 relative before:bg-[#00000AA] bg-cover rounded-b-lg">
            <div class="absolute inset-0 bottom-0 bg-[#0000000A]">
              <p class="text-lg font-bold text-white ml-5 mt-5">Now Season 11</p>
              <p class="text-xl font-bold text-white ml-5">アナーキー・イン・ザ・インターネット</p>
              <p class="text-white font-sm ml-5 opacity-80">部屋で俺、思想犯。部屋で俺、革命犯。</p>
            </div>
          </div>
        </div>
      </div>

      <div class="text-[#00000000]">半径0mの世界を変える 革命起こす幕開けの夜</div>
    </main>

    <main class="flex-1 flex flex-col" v-show="tab == 1">
      <div class="mt-4 h-15 border border-gray-300 rounded-t-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700">
        <div class="flex m-2 input">
          <input type="text" placeholder="履歴を検索" v-model="input" @keydown.enter="constract"
            class="flex-grow bg-white border border-gray-300 border-r-0 text-black px-4 py-2 rounded-l-md focus:outline-none placeholder:text-neutral-400 dark:bg-neutral-800 dark:border-neutral-700 dark:text-white" />

          <button
            class="py-1 px-3 text-base font-semibold transition-colors border-gray-300 border border-x-0 bg-white dark:bg-neutral-800 dark:border-neutral-700"
            @click="input = ''; constract()" v-show="!input == ''">
            <img src="/images/plus-circle-fill.svg" class="w-4 opacity-70 hover:opacity-100 rotate-45 dark:invert">
          </button>

          <button class="bg-black px-2 py-2 rounded-r-md dark:bg-blue-700" @click="constract">
            <img src="/images/arrow-up-right-circle.svg">
          </button>
        </div>
      </div>
      <ul class="pt-4 bg-neutral-50 rounded-b-lg dark:bg-neutral-900 border dark:border-neutral-700 border-t-0">
        <li v-for="trend in trends" :key="trend.id" class="mb-4 px-5">
          <div class="flex items-center justify-between">
            <span class="font-semibold text-black text-lg dark:text-white">{{ trend.text }}</span>
            <button class="text-neutral-300">
              <span class="text-neutral-400 text-sm mr-2">{{ trend.chat }}</span>
              <img src="/images/arrow-up-right-circle.svg"
                class="invert transform rotate-90 inline-block w-4 opacity-70 dark:invert-0">
            </button>
          </div>
          <p class="text-sm">{{ trend.sub }}</p>
        </li>
      </ul>
    </main>

    <main class="flex-1 flex flex-col" v-show="tab == 2">
      <div class="mt-4 h-22 border border-gray-300 rounded-t-lg bg-gray-100 dark:bg-[#1e1e1e] dark:border-neutral-700">
        <div class="bg-[url('/images/acheader.png')] w-full h-40 relative before:bg-[#0000000A] rounded-t-lg">
          <div class="absolute inset-x-0 bottom-0 h-1/3 bg-gradient-to-b from-transparent to-black">
            <img src="/images/user.png" class="w-28 ml-5">
          </div>
        </div>
      </div>
      <ul class="pt-4 bg-neutral-50 rounded-b-lg dark:bg-neutral-900 border dark:border-neutral-700 border-t-0 mb-24">
        <button class="bg-black text-white py-2 px-8 rounded-full font-bold ml-auto block mr-5">プロフィールを編集</button>

        <div class="ml-5 mt-5 mb-5">
          <h2 class="font-bold text-2xl dark:text-white">すい@alterna</h2>
          <p>@sui.onsen.ethereum.org</p>

          <div class="flex space-x-4 mt-2">
            <p><span class="text-bold dark:text-white mr-1">1</span>インスタンス</p>
            <p><span class="text-bold dark:text-white mr-1">Lv53</span>シーズン</p>
            <p><span class="text-bold dark:text-white mr-1">1290</span>リンク</p>
            <p><span class="text-bold dark:text-white mr-1">82</span>投稿</p>
          </div>
        </div>

        <div class="border-y boder-t-0 dark:border-neutral-700">
          <p class="ml-5 mt-5">トランザクション</p>
          <li v-for="tran in trans" :key="tran.id" class="mb-4 px-5 mt-1">
            <div class="flex items-center justify-between">
              <span class="font-semibold text-black text-lg dark:text-white">{{ tran.text }}</span>
              <button class="text-neutral-300">
                <span class="text-neutral-400 text-sm mr-2">{{ tran.chat }}</span>
                <img src="/images/arrow-up-right-circle.svg"
                  class="invert transform rotate-90 inline-block w-4 opacity-70 dark:invert-0">
              </button>
            </div>
            <p class="text-sm">{{ tran.sub }}</p>
          </li>
        </div>

        <div class="border-t-1 bg-neutral-50 dark:bg-neutral-900">
          <p class="ml-5 mt-5">コミュニティ</p>
          <li v-for="community in communitys" :key="community.id" class="mb-4 px-5 mt-1">
            <div class="flex items-center justify-between">
              <span class="font-semibold text-black text-lg dark:text-white">{{ community.text }}</span>
              <button class="text-neutral-300">
                <span class="text-neutral-400 text-sm mr-2">{{ community.chat }}</span>
                <img src="/images/arrow-up-right-circle.svg"
                  class="invert transform rotate-90 inline-block w-4 opacity-70 dark:invert-0">
              </button>
            </div>
            <p class="text-sm">{{ community.sub }}</p>
          </li>
        </div>
      </ul>

      <div class="text-[#00000000]">半径0mの世界を変える 革命起こす幕開けの夜</div>
    </main>

    <aside class="w-96 text-black">
      <div class="mt-4 ml-4 h-15 rounded-lg p-5 relative overflow-hidden"
        style="background: linear-gradient(258.56deg, #5FEE83 27.54%, #5FEEBB 103.89%)">
        <img src="/images/logo1.svg" class="invert w-36">
        <p class="text-xs mt-1">大体こんな感じっていうビジョンサイト</p>

        <p class="font-bold mt-2">水Protocolの概要</p>
        <div class="text-xs z-2">
          水ProtocolはwwwにSNSの機能を付け加えたものです。
          コレにより分散的で文化的なインターネットを。<br>
          ハイパーリンクを入力で機能を利用可能
          <br>
          tailaスキームを利用すると、このページの<br>グローバルやダイレクト、トレンドそして<br>所属するインスタンスに表示されます。
          <br>
          盛り上がってるサイトなどがわかりリアル<br>タイムなインターネットを楽しめます。
        </div>

        <img src="/images/Mascot.svg" class="position absolute w-40 right-[-2rem] bottom-[-3.2rem] z-1">
      </div>

      <div class="mt-4 ml-4 h-15 rounded-lg p-5 bg-neutral-50 dark:bg-neutral-800 border dark:border-neutral-700 dark:text-white">
        <p class="font-bold">試しに左のインプットに入力してみよう！</p>
        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.share</code>
        <div class="text-xs opacity-70">
          Webサイトそしてネット上の情報を拡散できる。
          この拡散時にテーマをインポートとその他のリンク機能を指定することによって情報が入り乱れるネット空間を楽しめる。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.chat</code>
        <div class="text-xs opacity-70">
          このハイパーリンク一つで様々なメディアにチャット画面を表示させることができる。
          チャットを展開したページが掲示板のスレッドのように扱われれ、このページのグローバル等に表示される。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.vc</code>
        <div class="text-xs opacity-70">
          このハイパーリンク一つで様々なメディアにボイスチャット画面を表示させることができる。
          テキストよりもよりリアルタイムに雑談ができる。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.vote</code>
        <div class="text-xs opacity-70">
          投票が行える。
          コレによりサイトに加えてほしい変更や意見などがわかりやすくなる。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.radio</code>
        <div class="text-xs opacity-70">
          音楽配信やラジオを投稿することができる。
          自分の作成したWebサイトにハイパーリンクとして埋め込むことができ、スマートコンストラクタ無しに分散のバックエンドシステムを使える。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.post</code>
        <div class="text-xs opacity-70">
          Twitterのように短文投稿ができる。
          グローバルやダイレクト、トレンド、所属インスタンスなどに表示される。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.dm</code>
        <div class="text-xs opacity-70">
          ダイレクトメッセージを送信できる。
          これにより直接のプライベートな会話ができる。
        </div>

        <code class="mt-3 mb-2 inline-block bg-[#ffffffba] text-sm dark:bg-[#ffffff0F] dark:border dark:border-neutral-700">taila://api.createsites</code>
        <div class="text-xs opacity-70">
          マークダウンとあらかじめ用意されたテーマ、そしてハイパーリンクの埋め込みによって高度なWebサイトをつくることができる。
          IPFSを利用してホスティングされる。
        </div>
      </div>
    </aside>
  </div>

  <div
    class="position fixed bottom-0 left-0 right-0 p-4 text-neutral-700 dark:text-neutral-500 text-xs bg-white border-t border-neutral-200 dark:bg-neutral-800 dark:border-neutral-700">
    <div class="flex flex-wrap justify-center gap-4">
      <img src="/images/twitter.svg" class="invert dark:invert-0"><span>@alterna_sui</span>
      <img src="/images/envelope-at.svg" class="invert dark:invert-0"><span>shadow.wizard.alterna@gmail.com</span>
      <span>水Protocol</span>
      <span>部屋の中革命犯、アナーキー・イン・ザ・1k</span>
      <span>ワールドワイドウェブに恋をした。</span>
      <span>Return Culture</span>
    </div>
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

code {
  border-radius: 3px;
  font-family: courier, monospace;
  padding: 0 3px;
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