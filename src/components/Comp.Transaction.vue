<script setup lang="ts">
import { defineProps } from "vue";
import { TransactionTypes } from "../types";

const emit = defineEmits(["deleteTransaction"]);

defineProps({
  transactions: {
    type: Array as () => TransactionTypes[],
    required: true,
  },
});

const handleDelete = (tId: string) => {
  emit("deleteTransaction", tId);
};
</script>

<template>
  <h1>this is transaction</h1>
  <ul class="list">
    <li
      v-for="t in transactions"
      :key="t.id"
      :class="t.price < 0 ? 'minus' : 'plus'"
    >
      {{ t.id }}
      {{ t.name }}
      {{ t.price }}

      <button @click="handleDelete(t.id)">delete</button>
    </li>
  </ul>
</template>

<!-- new setup header way -->
<!-- <script setup lang="ts">
const transactions = [
  {
    id: 1,
    name: "ak",
    price: 100,
  },
  {
    id: 61,
    name: "usp",
    price: -100,
  },
  {
    id: 2,
    name: "m4",
    price: 200,
  },
  {
    id: 3,
    name: "scar",
    price: 300,
  },
  {
    id: 4,
    name: "awp",
    price: 400,
  },
];
</script> -->

<!-- setup way -->
<!-- setup() {
    const transactions = [
      {
        id: 1,
        name: "ak",
        price: 100,
      },
      {
        id: 61,
        name: "usp",
        price: -100,
      },
      {
        id: 2,
        name: "m4",
        price: 200,
      },
      {
        id: 3,
        name: "scar",
        price: 300,
      },
      {
        id: 4,
        name: "awp",
        price: 400,
      },
    ];

    return { transactions };
  }, -->

<!-- export default way -->
<!-- 
  export default {
    data() {
      return {
        transactions: [
          {
            id: 1,
            name: "ak",
            price: 100,
          },
          {
            id: 61,
            name: "usp",
            price: -100,
          },
          {
            id: 2,
            name: "m4",
            price: 200,
          },
          {
            id: 3,
            name: "scar",
            price: 300,
          },
          {
            id: 4,
            name: "awp",
            price: 400,
          },
        ],
      };
    },
  }; -->
