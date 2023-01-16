<script setup>
import { ref } from "vue";
import MemoForm from "./components/MemoForm.vue";

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

function doneEdit() {
  editingMemo.value = null;
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

  <MemoForm
    v-if="editingMemo"
    v-model:content="editingMemo.content"
    @save="doneEdit"
  >
  </MemoForm>
</template>

<style scoped></style>
