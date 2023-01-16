<script setup>
import { ref } from "vue";

let id = 0;

const memos = ref([]);
const editingMemo = ref();

function addMemo() {
  const memo = { id: id++, content: "新規メモ" };
  memos.value.push(memo);
}

function editMemo(memo) {
  editingMemo.value = memo;
}
</script>

<template>
  <ul>
    <li v-for="memo in memos" :key="memo.id">
      <a @click.prevent="editMemo(memo)" href="#">{{ memo.content }}</a>
    </li>
  </ul>
  <form @submit.prevent="addMemo">
    <button>新規作成</button>
  </form>
  <div v-if="editingMemo">
    <div>
      <textarea v-model="editingMemo.content"></textarea>
    </div>
    <div>
      <button>編集</button>
    </div>
  </div>
</template>

<style scoped></style>
