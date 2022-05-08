<template>
    <h2>スロットテンプレート</h2>

    <h2>複数スロット</h2>
    <p>1つ目 name指定あり</p>
    <slot name="slot1"></slot>
    <p>2つ目 name指定なし</p>
    <slot></slot>
    <p>3つ目 name指定あり</p>
    <slot name="slot3">これは子での初期値</slot>

    <h2>スロットで親に値を渡す</h2>
    <p>nameとそれ以外一つあり</p>
    <slot name ="slot4" message="slotからのメッセージ1"></slot>
    <p>nameはなしでそれ以外二つあり</p>
    <slot message2="slotからのメッセージ2" message3="slotからのメッセージ3"></slot>

</template>

<script setup>

</script>

<style>

</style>