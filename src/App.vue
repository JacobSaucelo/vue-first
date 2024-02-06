<script setup lang="ts">
import Header from "./components/Header.vue";
import CompTransaction from "./components/Comp.Transaction.vue";

import { ref, computed, onMounted } from "vue";
import { TransactionAddType, TransactionTypes } from "./types";
import { useToast } from "vue-toastification";

import CompBalance from "./components/Comp.Balance.vue";
import CompExpenses from "./components/Comp.Expenses.vue";
import CompAddTransaction from "./components/Comp.AddTransaction.vue";

const transactions = ref<TransactionTypes[]>([]);

onMounted(() => {
  const savedTransactions = JSON.parse(
    // @ts-ignore
    localStorage.getItem("vue-transactions")
  );

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const toast = useToast();

const total = computed(() => {
  return transactions.value.reduce((acc, t) => {
    return acc + t.price;
  }, 0);
});

const income = computed(() => {
  return transactions.value
    .filter((t) => t.price > 0)
    .reduce((acc, t) => {
      return acc + t.price;
    }, 0);
});

const expenses = computed(() => {
  return transactions.value
    .filter((t) => t.price < 0)
    .reduce((acc, t) => {
      return acc + t.price;
    }, 0);
});

const handleTransaction = (t: TransactionAddType) => {
  const uuid = generateUniqueId();

  transactions.value.push({
    id: uuid,
    name: t.name,
    price: t.price,
  });

  saveToLocal();

  toast.success("successfully added transaction " + uuid);
};

const handleDelete = (tId: string) => {
  transactions.value = transactions.value.filter((t) => t.id !== tId);

  saveToLocal();

  toast.success("Deleted Sucessfully " + tId);
};

const generateUniqueId = () => {
  return self.crypto.randomUUID();
};

const saveToLocal = () => {
  localStorage.setItem("vue-transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <Header />

  <div class="container">
    <CompBalance :bal="+total" />
    <CompTransaction
      :transactions="transactions"
      @deleteTransaction="handleDelete"
    />
    <CompExpenses :income="+income" :expenses="+expenses" />
    <CompAddTransaction @transactionSubmitted="handleTransaction" />
  </div>
</template>
