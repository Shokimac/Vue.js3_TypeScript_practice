<script setup lang="ts">
import { defineProps } from 'vue';
type Tweet = {
  id: number,
  description: string
}
// 子側では、受け取ったPropsの値は変更することなくただ表示するだけとすれば綺麗なアプリケーションになる
// Propsは基本的には受け取って表示するだけ
type Props = {
  tweets: Tweet[]
}
const deleteTweet = (id: number) => {

}

defineProps<Props>()
</script>

<template>
  <!-- v-for の書き方は、取り出した中身を格納する変数 in 配列orオブジェクト で書く -->
  <!-- :key="tweet.id" で要素数分liタグを生成できる -->
  <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
    <span>{{ tweet.description }}</span>
    <button @click="deleteTweet(tweet.id)" class="delete-button">Delete</button>
  </li>
</template>

<style scoped>
.delete-button {
  color: #fff;
  font-weight: bold;
  background-color: #c99a68;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.delete-button:hover {
  background-color: #9d6324;
}

.tweet-list {
  list-style: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 12px;
  display: flex;
  justify-content: space-between;
  background-color: rgb(204, 2219, 233);
  padding: 8px 20px;
  width: 300px;
}
</style>