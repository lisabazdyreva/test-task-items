<script setup lang="ts">
import { computed } from "vue";
import ItemList from "@/components/common/ItemList.vue";

import type { IItem } from "@/types/item";

const props = defineProps<{
  data: Array<IItem> | null;
  maxItems: number;
}>();

const emits = defineEmits<{
  (e: "item-select", item: IItem): void;
}>();

const countCaption = computed(
  () => `${props.data?.length || 0} / ${props.maxItems} items`,
);

const handleItemSelect = (item: IItem) => {
  emits("item-select", item);
};
</script>

<template>
  <div class="user-items">
    <ItemList
      v-if="data?.length"
      class="user-items__list"
      :items="data"
      @item-select="handleItemSelect"
    />
    <p class="user-items__caption" v-else>None</p>
    <p class="user-items__caption">
      {{ countCaption }}
    </p>
  </div>
</template>

<style scoped>
.user-items__caption {
  padding: 10px;
}
</style>
