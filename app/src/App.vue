<script setup>
import { ref } from "vue";

let id = 0;

const memos = ref([]);

function addMemo() {
  const memo = { id: id++, content: "新規メモ" };
  memos.value.push(memo);
}
</script>

<template>
  <ul>
    <li v-for="memo in memos" :key="memo.id">
      {{ memo.content }}
    </li>
  </ul>
  <form @submit.prevent="addMemo">
    <button>新規作成</button>
  </form>
</template>

<style scoped></style>
