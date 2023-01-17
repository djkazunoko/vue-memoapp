<script setup>
import { ref } from "vue";
import MemoForm from "./components/MemoForm.vue";

let id = 0;
const STORAGE_KEY = "vue-memoapp";
const memos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]"));
const editingMemo = ref();

function addMemo() {
  const memo = { id: id++, content: "新規メモ" };
  memos.value.push(memo);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(memos.value));
}

function editMemo(memo) {
  editingMemo.value = memo;
}

function doneEdit() {
  editingMemo.value.content = editingMemo.value.content.trim();
  localStorage.setItem(STORAGE_KEY, JSON.stringify(memos.value));
  if (!editingMemo.value.content) {
    removeMemo();
  }
  editingMemo.value = null;
}

function removeMemo() {
  memos.value = memos.value.filter((memo) => memo !== editingMemo.value);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(memos.value));
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
    @remove="removeMemo"
  >
  </MemoForm>
</template>

<style scoped></style>
