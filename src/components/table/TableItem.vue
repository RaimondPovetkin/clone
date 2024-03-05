<template>
  <tr class="tr-class">
    <td class="text-left">
      <!-- <span>{{level}}</span> -->

        <q-icon v-if="item.subItems" name="arrow_drop_down" />

      <span :style="'padding-left:' + (level * 20) + 'px'">{{item.fat}}</span>

      <q-btn v-if="!item.subItems" size="xs" @click="addItemThis"><q-icon name="add" /></q-btn>
      {{ level }}<span></span>

    </td>
    <td class="text-right">{{item.calories}}</td>
    <td class="text-right">{{item.name}}</td>
    <td class="text-right">{{item.iron}}</td>
    <td class="text-right">{{item.calcium}}</td>
    <td class="text-right">{{item.sodium}}</td>
  </tr>

    <TableItem
      v-for="(i,index) in item.subItems"
      :item="i"
      :key="index"
      :level="level +1"
    >
    </TableItem>



</template>

<script setup lang="ts">
import { ref } from 'vue';
import TableItem from 'src/components/table/TableItem.vue';

const emit = defineEmits(['addItem'])

function addItemThis(){
  console.log(props.item)
  props.item.subItems = [
      {
      name: 'Eclair',
      calories: 262,
      fat: 16.0,
      carbs: 23,
      protein: 6.0,
      sodium: 337,
      calcium: '6%',
      iron: '7%',
      children: 10
    },
    {
      name: 'Cupcake',
      calories: 305,
      fat: 3.7,
      carbs: 67,
      protein: 4.3,
      sodium: 413,
      calcium: '3%',
      iron: '8%'
    },
  ]
}

const props = defineProps({
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
  transition: display 0.3 s ease;
}
</style>
