<!-- 親から子への引き渡し用 -->

<template>
    <h2 v-bind:style="$attrs.style">さようならこれはPタグです</h2>
    {{oyahe.message}}
    {{oyahe.name}}
    <!-- {{oyatatihe.messages}} -->
    <p v-bind:id="$attrs.id">ここから数値、真偽値、変数のprops</p>
    {{oyahe.price + 1000}}
    <p v-if="oyahe.iserror" class="small" v-bind:class="$attrs.class">ISERRORです。</p>
        <p v-else v-bind:class="$attrs.class">ISERRORではなかったです。</p>
</template>



<script setup>
// １ーpropsの定義（変数とその型を指定する。複数可。デフォルト可能。親での指定必須設定可能）
    const oyahe = defineProps({
    message:String,
    name: { type: String, default: '親が決めてくれなかったとき用の名前', required:true},
    price:Number,
    iserror:Boolean
})
// ２－propsの定義（配列として指定する）
    // const oyatatihe = defineProps(['messages']);

</script>



<style>

</style>