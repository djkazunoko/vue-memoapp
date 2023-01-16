<script setup>
defineProps({ content: String });
defineEmits(["update:content", "save"]);
</script>

<template>
  <div>
    <textarea
      :value="content"
      @input="$emit('update:content', $event.target.value)"
    ></textarea>
  </div>
  <button @click="$emit('save')">編集</button>
</template>
