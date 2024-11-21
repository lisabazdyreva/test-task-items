<script setup lang="ts">
import type { IItem } from "@/types/item";

defineProps<{
  items: Array<IItem>;
}>();

defineEmits<{
  (e: "item-select", item: IItem): void;
}>();
</script>

<template>
  <ul class="item-list">
    <li class="item-list__item" v-for="item in items" :key="item.id">
      <button class="item-list__button" @click="$emit('item-select', item)">
        {{ item.name }}
      </button>
    </li>
  </ul>
</template>

<style scoped>
.item-list {
  margin: 0;
  padding: 10px;
  list-style: none;
}

.item-list__item {
  margin-bottom: 10px;
  &:last-child {
    margin-bottom: 0;
  }
}

.item-list__button {
  border: none;
  font: inherit;
  border-radius: 4px;
  color: #000000;
  background-color: #cecece;
  cursor: pointer;
  padding: 0.5rem 1rem;

  &:hover {
    background-color: #dedede;
  }
}
</style>
