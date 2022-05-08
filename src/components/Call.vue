<template>
    <h2>emitを使う子コンポーネント</h2>
    <p>この部分をボタンクリック時に、親の操作で書き換える</p>
    <p>{{props.hungry}}</p>
    <button @click="sendNote">おなかいっぱい用ボタン</button>
    <button @click="sendNote2">エミット用ボタン2</button>
    <p>入力フォーム</p>
    <input type="text" v-model="name" @input="changeName">
    <p>これは子のテンプレ上のname：{{name}}</p>

</template>

<script setup>
import { ref } from 'vue';

    // 通知イベント名を定義しておかないと、テンプレートのルートタグが複数あるときは警告が出る。
    // また、イベントを複数使うには定義しておく必要がある？
    const emit = defineEmits(['note', 'note2', 'note3']);
    //通知イベントと同時に他の処理も入れることができる
    // emitはタグ内で使うときは$emitだが、ここで使う場合はemitでよい
    const sendNote = () => {
        emit("note");
    }
    const sendNote2 = () => {
        alert("2つの通知が送られます");
        emit("note2", {firstName:"totti" , familyName:"franchesco"});
        emit("note3");
    }

     //propsの定義
    const props = defineProps({
        hungry:String,
        name:String
    })
    // 親にnameを渡す
    const name = ref("初期name");
    const changeName = () => {
        emit("noteChange", name.value)
    }




</script>

<style>

</style>