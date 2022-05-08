<script setup>
import { inject } from 'vue';

const { message } = defineProps(['messageB']);
const message2 = inject('messageInject');

</script>



<template>
  <h3>TestBコンポーネント</h3>
  <p>{{ messageB }}</p>
  <p>{{ message2 }}</p>
</template>

<style>

</style>