<template>
  <h1>income: {{ income }}</h1>
  <h1>expenses: {{ expenses }}</h1>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
  income: {
    type: Number,
    required: true,
  },

  expenses: {
    type: Number,
    required: true,
  },
});
</script>
