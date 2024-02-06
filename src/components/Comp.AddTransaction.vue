<script setup lang="ts">
import { ref } from "vue";

import { useToast } from "vue-toastification";
import { TransactionAddType } from "../types";

const name = ref("");
const price = ref("");

const emit = defineEmits(["transactionSubmitted"]);

const toast = useToast();

const handleSubmit = () => {
  if (!name.value || !price.value) {
    toast.error("Both fields must be filled.");
    return;
  }

  const data: TransactionAddType = {
    name: name.value,
    price: parseFloat(price.value),
  };

  emit("transactionSubmitted", data);

  name.value = "";
  price.value = "";
};
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="name" />
    <input type="text" v-model="price" />
    <button>submit</button>
  </form>
</template>
