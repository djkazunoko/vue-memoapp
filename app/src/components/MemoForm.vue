<script setup>
import { ref, onMounted, onUpdated } from "vue";

defineProps({ content: String });
defineEmits(["update:content", "save", "remove"]);

const textarea = ref(null);

onMounted(() => {
  textarea.value.focus();
});

onUpdated(() => {
  textarea.value.focus();
});
</script>

<template>
  <div>
    <textarea
      cols="30"
      rows="10"
      :value="content"
      @input="$emit('update:content', $event.target.value)"
      ref="textarea"
      placeholder="文字を入力してください"
    ></textarea>
    <div>
      <button @click="$emit('save')">保存</button>
      <button @click="$emit('remove')">削除</button>
    </div>
  </div>
</template>

<style scoped>
button {
  margin-right: 10px;
  cursor: pointer;
}
</style>
