<template>
  <h1>balance {{ bal }}</h1>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
  bal: {
    type: Number,
    required: true,
  },
});
</script>
