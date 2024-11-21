<script setup lang="ts">
import type { IItem } from "@/types/item";

defineProps<{
  item: IItem | null;
}>();

defineEmits<{
  (e: "item-select"): void;
}>();
</script>

<template>
  <div class="selected-item">
    <div class="selected-item__wrapper" v-if="item">
      {{ item.name }}

      <button class="selected-item__button" @click="$emit('item-select')">
        Clear
      </button>
    </div>
    <p v-else>None</p>
  </div>
</template>

<style scoped>
.selected-item__wrapper {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.selected-item__button {
  margin-top: auto;
  margin-bottom: 15px;
  border: none;
  font: inherit;
  border-radius: 4px;
  color: #000000;
  background-color: #cecece;
  cursor: pointer;
  padding: 0.5rem 1rem;
  align-self: center;

  &:hover {
    background-color: #dedede;
  }
}
</style>
