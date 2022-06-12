<script setup lang="ts">
import { ref } from 'vue'
import TweetPostForm from './TweetPostForm.vue';
import TweetList from './TweetList.vue';
// 静的な状態で v-forを使い一つ一つを取り出す
// const tweets = [{ id: '0', description: 'Hello, world!' }, { id: '1', description: 'This is second tweet.' }]
const tweets = ref([{ id: 0, description: 'Hello, world!' }, { id: 1, description: 'This is second tweet.' }])
const inputtingDescription = ref<string>('')

const postTweet = () => {
  const tweet = { id: Math.random(), description: inputtingDescription.value }
  tweets.value.push(tweet)
  inputtingDescription.value = ''
  console.log('post...', tweets.value)
}

const deleteTweet = (id: number) => {
  // filterの引数内 t には、tweetsの各要素が入る
  tweets.value = tweets.value.filter(t => t.id !== id)
}
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <TweetPostForm />
    <div class="tweet-container">
      <!-- v-if とは別で、v-showを使って条件がtrueの時のみ表示させることもできる -->
      <!-- <p v-show="tweets.length <= 0">No tweets have been added</p> -->
      <p v-if="tweets.length <= 0">No tweets have been added</p>
      <ul v-else>
        <!-- TweetList側でPropsを宣言することで、値の受け渡しを可能にする -->
        <TweetList :tweets="tweets" />
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  margin-bottom: 16px;
}
</style>