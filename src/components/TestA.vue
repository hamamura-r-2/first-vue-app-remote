<script setup>
import TestB from './TestB.vue';

const { message } = defineProps(['messageA']);
</script>


<template>
  <h2>TestAコンポーネント</h2>
  <TestB :messageB="messageA" />
</template>

<style>

</style>