<script setup>
import { ref, onMounted } from "vue";

defineProps({ content: String });
defineEmits(["update:content", "save", "remove"]);

const textarea = ref(null);

onMounted(() => {
  textarea.value.focus();
});
</script>

<template>
  <div>
    <textarea
      :value="content"
      @input="$emit('update:content', $event.target.value)"
      ref="textarea"
    ></textarea>
  </div>
  <button @click="$emit('save')">編集</button>
  <button @click="$emit('remove')">削除</button>
</template>
