<template>
  <v-container class="text-center">
    <v-row class="text-center">
      <v-col cols="12"> <h3> Equipments </h3> </v-col>
      
      <div class="d-flex align-content-center flex-wrap pa-0 text-center" style="width: 200px !important;">
        <v-col 
          v-for="(item, idx) in $items" 
          :class="getPaddingItemSlot(item.slot)"
          :key="idx"
          class="pa-0"
          cols="4"
        > 
          <v-tooltip top>
            <template v-slot:activator="{ on, attrs }">
              <img 
                :src="require(`~/assets/images/items/${getItem(item.id, item.slot)}.gif`)"
                width="32"
                height="32"
                v-bind="attrs"
                v-on="on"
              />
            </template>
            <span> {{ getItemName(item.id, item.slot) }} </span>
          </v-tooltip>
        </v-col>
      </div>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'
import { character } from '@/store'
import { Item } from '@/models'
import { items } from '@/utils/fakeData'

export default Vue.extend({
  computed: {
    $items(): Item[] {
      return character.$items;
    },

    getItemList(): Object[] {
      return items;
    },
  },

  methods: {
    getPaddingItemSlot(slot: String): String {
      switch(slot) {
        case 'necklace':
          return 'pt-3';
        case 'backpack':
          return 'pt-3';
        case 'armor':
          return 'pb-2';
        case 'legs':
          return 'pt-0';
        case 'boots':
          return 'pt-0';
        default:
          return "";
      }
    },
    
    getItem(this: any, id: Number, slot: String) {
      return this.getItemList.some((item: Item) => item.id === id)
        ? this.getItemList.find((item: Item) => item.id === id).id
        : slot;
    },

    getItemName(this: any, id: Number, slot: String) {
      return this.getItemList.some((item: Item) => item.id === id)
        ? this.getItemList.find((item: Item) => item.id === id).name
        : "No_" + slot;
    },
  }
})
</script>