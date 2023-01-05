<script setup>
import { ref, computed } from 'vue';
import Card from './components/Card.vue'
const items = ref([
  {
    id: 1,
    name: 'アボカドソースバケット',
    description: '刻んだ野菜をアボカドと混ぜ、優しいソースに。こんがり焼いたバゲットとお召し上がりください。',
    price: 320,
    image: '/images/item1.jpg',
    soldOut: false,
    selected: false,
  },
  {
    id: 2,
    name: 'あの日見たホットケーキ',
    description: '子供の頃に食べたかった、あのホットケーキを再現しました。素朴でどこか懐かしい味をどうぞ。',
    price: 1180,
    image: '/images/item2.jpg',
    soldOut: false,
    selected: false,
  },
  {
    id: 3,
    name: 'HOP WTR',
    description: 'ロサンゼルス生まれのスパーリングウォーター。ノンカロリー。ノンアルコールの新感覚飲料です。',
    price: 320,
    image: '/images/item3.jpg',
    soldOut: false,
    selected: false,
  },
  {
    id: 4,
    name: 'チーズフレンチフライ',
    description: 'イタリア産のチーズをたっぷりかけた熱々のフレンチフライ。みんな大好きな一品です。',
    price: 670,
    image: '/images/item4.jpg',
    soldOut: false,
    selected: false,
  }
])

// 在庫のある商品数を返す　関数
// const stockQuantity = () => {
//   return items.value.filter(item => item.soldOut === false).length
// }
// 在庫のある商品数を返す 算出プロパティ
const stockQuantityComputed = computed(() => {
  return items.value.filter(item => item.soldOut === false).length
})

// 商品の在庫状況を変更する 関数
const stockItem = (item) => {
  item.soldOut = false;
}

//現在時刻を表示する 関数
const getDate = () => {
  const date = new Date();
  return date;
}

//現在時刻を表示する 算出プロパティ
const getDateComputed = computed(() => {
  const computedDate = new Date();
  return computedDate;
})

const changeSoldOut = (id) => {
  const pickElm = items.value.find(item => item.id == id)
  pickElm.soldOut = true;
}

</script>

<template>
  <header class="header">
    <img src="/images/logo.svg" alt="" class="">
    <h1 class="">商品データ管理ページ</h1>
  </header>
  <div>商品数:{{ stockQuantityComputed }}</div>
  <div>現在時刻:{{ getDate() }}</div>
  <div>現在時刻:{{ getDateComputed }}(computed)</div>
  <main class="main">
    <template v-for="(item, index) in items" :key="item.id">
      <div class="item" v-if="!item.soldOut" :class="{ 'selected-item': item.selected }"
        @keyup.enter="item.selected = !item.selected" @click="item.selected = !item.selected" tabindex="0">
        <Card :id="item.id" :image="item.image" :name="item.name" :description="item.description" :price="item.price"
          @sold-out="changeSoldOut" />
      </div>
      <div v-else>売り切れです<button type="button" @click="stockItem(item)">入荷</button></div>
    </template>
  </main>
</template>

<style>
body {
  font-family: sans-serif;
  margin: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  width: 90%;
  margin: 10px 5%;
  color: #242424;
}

.header>img {
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.header>h1 {
  font-size: 80px;
  font-weight: bold;
  line-height: 80px;
  margin-top: 0;
  margin-bottom: 20px;
}

.main {
  display: grid;
  grid-template-columns: 3fr 3fr 3fr 3fr;
  column-gap: 24px;
  row-gap: 24px;
}

.item {
  padding: 10px;
  cursor: pointer
}

.item:hover {
  transition: 0.2s transform ease-out;
  transform: scale(1.05);
}

.selected-item {
  background-color: #e3f2fd;
}
</style>
