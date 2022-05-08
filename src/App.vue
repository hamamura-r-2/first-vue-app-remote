<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
import Hello from './components/Hello.vue'
import Bye from './components/Bye.vue';
import Call from "./components/Call.vue";
import Slottest from "./components/SlotTest.vue"
import Tokyo from "./components/Tokyo.vue"
import Kyoto from "./components/Kyoto.vue"
import TestA from "./components/TestA.vue"


import { provide } from 'vue';

import { ref, computed } from 'vue';


const name = ref("Ken");
const changeName = () => {
  name.value = "KenKen"
}

const stomachState = ref("おなかすいた");
const eat = () => {
  stomachState.value = "おなかいっぱい";
}

const isClicked = () => {
    console.log("子コンポーネント1でクリックされました")
    eat();
}
const isClicked2 = (passName) => {
    console.log("子コンポーネント2でクリックされました")
    console.log(`${passName.familyName} ${passName.firstName}`)
}
const isClicked3 = () => {
    console.log("子コンポーネント3でクリックされました")
}

// 子からもらった値を使ってデータ更新する
const handleName = (passName) => {
  name.value = passName;
}

// Dynamicコンポーネント用
const city = ref('tokyo');
const tabs = {
  tokyo: Tokyo,
  kyoto: Kyoto,
};
const tab = computed(() => tabs[city.value]);

// provide用
provide('messageInject', 'Provide/Injectでデータ渡し');

</script>




<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + Vite" />
  <Hello/>
  <Hello/>
  <Hello/>
  <p><br><br><br></p>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>ここから下でpropsの利用</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <p>文字列のprops</p>
  <!-- １props使い方 -->
  <Bye message="これは親からの引き渡しメッセージ" v-bind:price="2000" v-bind:iserror="false" v-bind:name="name"/>
  <button v-on:click="changeName">親コンポーネントのname変更するボタン</button>
  <p>親コンポーネントで定義した変数を、子コンポーネントで更新してはいけない</p>

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>id,class,styleの引き渡しではprops不要</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <Bye class="big" id="you" style="color:red" message="仮" v-bind:price="2000" v-bind:iserror="true" v-bind:name="name" />

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>emitを使用</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <Call :hungry = "stomachState" @note="isClicked" @note2="isClicked2" @note3="isClicked3" @noteChange="handleName"/>
  <p>これは子コンポーネントで入力してもらった値を親のテンプレ上で表示しているだけ{{name}}</p>

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>inputをコンポーネント化して再利用</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>slot</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <Slottest>
     <template v-slot:default="slotprop1">
        これは親の方で直接書いた文。なければ初期値が適用される。
        <span style="font-weight: 900; font-size: 1.4em">htmlも挿入可能</span>
        {{slotprop1}}
     </template>

     <template v-slot:slot1>1用の親指定</template>
     <template v-slot:slot3></template>
     <template v-slot:slot4="slotprop1">{{slotprop1}}</template>
  </Slottest>

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>dynamicなんとか</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <p>なぜかis属性の値を変数直接ではなく、いったんオブジェクトをかませてからやらないといけない</p>
  <div>
    <button @click="city = 'tokyo'">東京</button>
    <button @click="city = 'kyoto'">京都</button>
  </div>
<keep-alive><component v-bind:is="tab"></component></keep-alive>

  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>
  <h2>孫へのpropsと、provideとinject</h2>
  <p>ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー</p>

  <h1></h1>
  <TestA messageA="propsでデータ渡し" />



  <!-- ２props使い方(配列指定) -->
  <!-- <Bye messages="これは配列propsの1つ目"/>
  <Bye messages="これは配列propsの2つ目"/> -->

</template>





<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
