<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs } from 'vue'

// 単一なものは refを使う
// const itemName1 = ref<string>('Desk')
// const itemPrice1 = 40000

// オブジェクトそのものなど複数に対してリアクティブにしたい場合は、 reactive()の引数にオブジェクトをセット
const item1 = reactive({
  name: 'Desk',
  price: 40000
})

const itemName2 = 'Bike'
const itemPrice2 = 20000

const url1 = 'https://www.google.co.jp/'

const buy = (itemName: string) => {
  alert('Are you sure to buy ' + itemName + ' ??')
}

// inputタグにv-modelを設定したので、必要なくなる
// const input = (event: any) => {
//   item1.name = event.target.value
// }

// inputタグにv-modelを設定したので、必要なくなる
// const inputPrice = (event: any) => {
//   item1.price = event.target.value
// }

const clear = () => {
  item1.name = ''
  item1.price = 0
}

const budget = 50000

// 何らかの条件を元に、値を生成する時に使うのが Vueのcomputed
// 条件分岐や計算など処理を用いて変数に値を格納する
// computed の中にアロー関数を入れる
// const priceLabel = computed(() => {
//   if (item1.price > budget) {
//     return 'too expensive...'
//   } else {
//     return item1.price + ' yen'
//   }
// })

// 上記のcomputedを下記のように単純にitem1.priceに依存した処理をメソッド内に書いても反映されるが
// Vueのcomputedを使うことで、キャッシュが効いたり動作が最適化されるメリットがあるとのことで、computedを使うことが推奨されている
// const getPriceLabel = () => {
//   if (item1.price > budget) {
//     return 'too expensive...'
//   } else {
//     return item1.price + ' yen'
//   }
// }

const priceLabel = ref<string>(item1.price + 'yen')
// item1のようにリアクティブなオブジェクトのプロパティは、Vueとしてはリアクティブではないものと認識されるため
// toRefs()にオブジェクトを渡して、そのプロパティをリアクティブな値として返すことで、watchの第一引数に各プロパティを設定させることができる
const { price } = toRefs(item1)
watch(price, () => {
  if (price.value > budget) {
    priceLabel.value = 'too expensive...'
  } else {
    priceLabel.value = price.value + ' yen'
  }
})

</script>

<template>
  <div class="container">
    <h1>Payment</h1>
    <!-- <input v-on:input="input" v-bind:value="item1.name" /> -->
    <!-- ↑これは ↓こう書くことができる。 inputタグのように双方向で値が変化する要素にはv-modelで簡潔に書ける -->
    <input v-model="item1.name">
    <input v-model="item1.price" />
    <button v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <!-- 下記のように三項演算子で書けるが、Vueの基本的な考え方として、template内にはロジックはあまり持たせない -->
      <!-- <label>{{ item1.price > budget ? 'too expensive...' : item1.price }}</label> -->
      <label>{{ priceLabel }}</label>
      <!-- <label>{{ item1.price }}円</label> -->
      <a v-bind:href="url1">bought at...</a>
      <button v-on:click="buy(item1.name)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label>
      <label>{{ itemPrice2 }}円</label>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: aliceblue;
  margin-bottom: 8px;
}

label {
  font-size: 20px;
  font-weight: bold;
}

input {
  margin-bottom: 8px;
}
</style>