<script setup lang="ts">
import { ref } from "vue";
import type { IItem } from "@/types/item.ts";

import userItemsMocks from "@/mocks/userItems.json";
import itemsMocks from "@/mocks/items.json";
import ItemList from "@/components/common/ItemList.vue";
import SelectedUserItemsComponent from "@/components/user-items/SelectedUserItems.vue";
import SelectedItemComponent from "@/components/item/SelectedItem.vue";

const MAX_USER_ITEMS = 6;

const userItems = userItemsMocks as IItem[];
const items = itemsMocks as IItem[];

const selectedUserItems = ref<IItem[] | null>(null);
const selectedItem = ref<IItem | null>(null);

const handleUserItemDeselect = (itemDeselect: IItem) => {
  if (!selectedUserItems.value?.length) {
    return;
  }

  const items = selectedUserItems.value.filter(
    (item) => item.id !== itemDeselect.id,
  );

  if (items.length > 0) {
    selectedUserItems.value = items;
    return;
  }
  selectedUserItems.value = null;
};

const handleItemDeselect = () => {
  selectedItem.value = null;
};

const handleUserItemSelect = (itemSelected: IItem) => {
  if (!selectedUserItems.value?.length) {
    selectedUserItems.value = [itemSelected];
    return;
  }

  const index = selectedUserItems.value.findIndex(
    (item) => item.id === itemSelected.id,
  );

  if (index < 0 && selectedUserItems.value.length < MAX_USER_ITEMS) {
    selectedUserItems.value = [...selectedUserItems.value, itemSelected];
    return;
  }

  selectedUserItems.value = selectedUserItems.value.filter(
    (item) => item.id !== itemSelected.id,
  );
};

const handleItemSelect = (item: IItem) => {
  selectedItem.value = selectedItem.value?.id === item.id ? null : item;
};
</script>

<template>
  <main>
    <div class="home-page">
      <SelectedUserItemsComponent
        class="home-page__selected-user-items"
        :data="selectedUserItems"
        :max-items="MAX_USER_ITEMS"
        @item-select="handleUserItemDeselect"
      />

      <SelectedItemComponent
        class="home-page__selected-item"
        :item="selectedItem"
        @item-select="handleItemDeselect"
      />

      <ItemList
        class="all-items__user-item-list"
        :items="userItems"
        @item-select="handleUserItemSelect"
      />
      <ItemList
        class="all-items__item-list"
        :items="items"
        @item-select="handleItemSelect"
      />
    </div>
  </main>
</template>

<style scoped>
.home-page {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 320px auto;
  row-gap: 50px;
  column-gap: 50px;

  & > div,
  & > ul {
    border: 2px solid #ccc;
    border-radius: 2px;
  }
}
</style>
