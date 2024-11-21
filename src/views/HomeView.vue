<script setup lang="ts">
import { ref } from "vue";
import type { IItem } from "@/types/item.ts";

import userItemsMocks from "@/mocks/userItems.json";
import itemsMocks from "@/mocks/items.json";

const userItems = userItemsMocks as IItem[];
const items = itemsMocks as IItem[];

const MAX_USER_ITEMS = 6;
const selectedUserItems = ref<Array<IItem> | null>(null);
const selectedItem = ref<IItem | null>(null);
</script>

<template>
  <main>
    <div class="home-page">
      <div class="home-page__selected-items selected-items">
        <div class="selected-items__user-items user-items">
          Слева - выбранные вещи из вещей пользователя (блок снизу-слева)
          <ul class="user-items__list">
            <li v-for="userItem in selectedUserItems" :key="userItem.id">
              {{ userItem.name }}
            </li>
          </ul>
          <span class="user-items__caption">
            {{ `${selectedUserItems?.length || 0} / ${MAX_USER_ITEMS}` }}
          </span>
          {{ selectedUserItems }}
        </div>

        <div class="selected-items__one-item one-item">
          <div class="one-item__wrapper">
            {{ selectedItem?.name }}
          </div>
        </div>
      </div>

      <div class="home-page__all-items all-items">
        <ul class="all-items__user-item-list user-item-list">
          <li>
            Снизу-слева можно выбрать от 1 до 6 вещей, которые должны
            отображаться в верхней левой части в порядке выбора.
          </li>
          <li
            class="user-item-list__item"
            v-for="userItem in userItems"
            :key="userItem.id"
          >
            {{ userItem.name }}
          </li>
        </ul>

        <ul class="all-items__item-list item-list">
          <li>
            Снизу-справа можно выбрать одновременно только 1 вещь, которая
            должна отображаться справа-сверху.
          </li>
          <li class="item-list__item" v-for="item in items" :key="item.id">
            {{ item.name }}
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>
