<template>
  <tr style="transition: all 1s;">
    <td class="text-left" style="transition: all 1s;">
      <!-- <span>{{level}}</span> -->

        <q-icon v-if="item.subItems" name="arrow_drop_down" />

      <span :style="'padding-left:' + (level * 20) + 'px'">{{item.fat}}</span>

      <q-btn v-if="item.canExpand" size="xs" @click="addItemThis(item)"><q-icon name="add" /></q-btn>
      {{ level }}<span></span>
      <q-btn v-if="item.subItems" size="xs" @click="removeItemThis(item)"><q-icon name="remove" /></q-btn>
      {{ item.isHided }}

    </td>
    <td class="text-right">{{item.calories}}</td>
    <td class="text-right">{{item.name}}</td>
    <td class="text-right">{{item.iron}}</td>
    <td class="text-right">{{item.calcium}}</td>
    <td class="text-right">{{item.sodium}}</td>
  </tr>

    <TableItem
      v-for="(i,index) in item.isHided ? [] : item.subItems"
      :item="i"
      :key="index"
      :level="level +1"
      @addItem="addItemThis"
      @removeItem="removeItemThis"
      >
    </TableItem>



</template>

<script setup lang="ts">
import { ref } from 'vue';
import TableItem from 'src/components/table/TableItem.vue';

const emit = defineEmits(['addItem','removeItem'])

function addItemThis(item){
  emit('addItem',item)
}

function removeItemThis(item){
  emit('removeItem',item)
}

const props = defineProps({
  hidedItems: {
    type: Array,
    required: false,
    default: ()=>{[]}
  },
  item: {
    type: Object,
    required: false,
    default: ()=>{{}}
  },
  level: {
    type: Number,
    required: true,
    default: ()=>{1}
  },
})

</script>
<style lang="scss">
.tr-class{
  transition: all 1s;
}
</style>
