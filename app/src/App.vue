<script setup>
import { ref } from "vue";
import MemoForm from "./components/MemoForm.vue";

const STORAGE_KEY = "vue-memoapp";
const memos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]"));
const editingMemo = ref();

function createMemo() {
  const memo = { id: Date.now(), content: "" };
  editMemo(memo);
}

function editMemo(memo) {
  editingMemo.value = { id: memo.id, content: memo.content };
}

function doneEdit() {
  editingMemo.value.content = editingMemo.value.content.trim();
  if (!editingMemo.value.content) {
    removeMemo();
  } else {
    const memo = memos.value.find((memo) => memo.id === editingMemo.value.id);
    if (memo) {
      memo.content = editingMemo.value.content;
    } else {
      memos.value.push(editingMemo.value);
    }
    localStorage.setItem(STORAGE_KEY, JSON.stringify(memos.value));
    editingMemo.value = null;
  }
}

function removeMemo() {
  memos.value = memos.value.filter((memo) => memo.id !== editingMemo.value.id);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(memos.value));
  editingMemo.value = null;
}

function getFirstLine(text) {
  return text.split(/\n/)[0];
}
</script>

<template>
  <form @submit.prevent="createMemo">
    <button>新規作成</button>
  </form>
  <div class="main">
    <ul>
      <li v-for="memo in memos" :key="memo.id">
        <a
          @click.prevent="editMemo(memo)"
          href="#"
          :class="memo.id === editingMemo?.id ? 'selected' : ''"
        >
          {{ getFirstLine(memo.content) }}
        </a>
      </li>
    </ul>

    <MemoForm
      v-if="editingMemo"
      v-model:content="editingMemo.content"
      @save="doneEdit"
      @remove="removeMemo"
    >
    </MemoForm>
  </div>
</template>

<style scoped>
.main {
  display: flex;
}
.main ul {
  padding-left: 0px;
  padding-right: 20px;
  margin: 0;
}
button {
  cursor: pointer;
}
form {
  margin-bottom: 1em;
}
.selected {
  color: inherit;
  text-decoration: none;
  pointer-events: none;
}
</style>
