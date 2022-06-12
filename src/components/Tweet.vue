<script setup lang="ts">
import { ref } from 'vue'
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
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
      <input v-model="inputtingDescription" />
      <button class="save-button" @click="postTweet()">post</button>
    </div>
    <div class="tweet-container">
      <ul>
        <!-- v-for の書き方は、取り出した中身を格納する変数 in 配列orオブジェクト で書く -->
        <!-- :key="tweet.id" で要素数分liタグを生成できる -->
        <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
          <span>{{ tweet.description }}</span>
        </li>
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

.save-button {
  color: #fff;
  font-weight: bold;
  background-color: #68c9c9;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.save-button:hover {
  background-color: #1baaaa;
}

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

input {
  margin-bottom: 16px;
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

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aliceblue;
  padding: 24px 0;
  width: 60%;
  margin-bottom: 12px;
  border-radius: 4px;
}
</style>