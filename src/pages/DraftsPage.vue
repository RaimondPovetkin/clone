<template>
  <q-page :style-fn="()=>{}" style="height: 100%;">{{ hidedItems }}

    <q-scroll-area style="width: 100%; height: 100%;">
    <q-markup-table separator="cell">
      <thead>
        <tr>
          <th class="text-left">Dessert (100g serving)</th>
          <th class="text-right">Calories</th>
          <th class="text-right">Fat (g)</th>
          <th class="text-right">Carbs (g)</th>
          <th class="text-right">Protein (g)</th>
          <th class="text-right">Sodium (mg)</th>
        </tr>
      </thead>
      <tbody style="transition: all 1s;">
          <TableItem @removeItem="removeItem" @addItem="addItem" v-for="(item, index) in rows" :key=index :hidedItems=hidedItems :item="item" :level="0"></TableItem>
      </tbody>
    </q-markup-table>
  </q-scroll-area>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import TableItem from 'src/components/table/TableItem.vue';


const hidedItems = ref([])

function recourseFindItem(items, id){
  for(let i in items){
    if(items[i].id === id){
      console.log('ura')
      return items[i]
    } else if (items[i].subItems){
      const findedItem = recourseFindItem(items[i].subItems, id)
      if(findedItem){
        return findedItem
      }
    }

  }

}

function removeItem(item){
  if(!hidedItems.value.find(i=>i === item.id)){
    hidedItems.value.push(item.id)
  }
  let foundItem = recourseFindItem(rows.value, item.id)
  foundItem.isHided = true
}

function addItem(item){
  //hidedItems.value = hidedItems.value.filter(i=>i !== item.id)
  let foundItem = recourseFindItem(rows.value, item.id)
  delete foundItem.isHided;
  if(foundItem && !hidedItems.value.find(i=>i === item.id)){
    setTimeout(()=>{
      foundItem.subItems=[
      {
        name: 'Lollipop',
        calories: 392,
        fat: 0.2,
        carbs: 98,
        protein: 0,
        sodium: 38,
        calcium: '0%',
        iron: '2%',
        id: Math.floor(Math.random() * 9998) + 2,
        canExpand: true,
      },
      {
        name: 'Honeycomb',
        calories: 408,
        fat: 3.2,
        carbs: 87,
        protein: 6.5,
        sodium: 562,
        calcium: '0%',
        iron: '45%',
        id: Math.floor(Math.random() * 9998) + 2,
        canExpand: true,
      },
      ]
    },2000)
  }
}

const columns = ref([
  {
    name: 'name',
    required: true,
    label: 'Dessert (100g serving)',
    align: 'left',
    field: row => row.name,
    format: val => `${val}`,
    sortable: true
  },
  { name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true },
  { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
  { name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
  { name: 'protein', label: 'Protein (g)', field: 'protein' },
  { name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
  { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
  { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
]);

const rows = ref([
  {
    name: 'Frozen Yogurt',
    calories: 159,
    fat: 6.0,
    carbs: 24,
    protein: 4.0,
    sodium: 87,
    calcium: '14%',
    iron: '1%',
    id: 1,
    canExpand: true,
  },
  {
    name: 'Ice cream sandwich',
    calories: 237,
    fat: 9.0,
    carbs: 37,
    protein: 4.3,
    sodium: 129,
    calcium: '8%',
    iron: '1%',
    id: 2,
    canExpand: false,
  },
  {
    name: 'Eclair',
    calories: 262,
    fat: 16.0,
    carbs: 23,
    protein: 6.0,
    sodium: 337,
    calcium: '6%',
    iron: '7%',
    children: 10,
    id: 9,
    canExpand: false,
  },
  {
    name: 'Cupcake',
    calories: 305,
    fat: 3.7,
    carbs: 67,
    protein: 4.3,
    sodium: 413,
    calcium: '3%',
    iron: '8%',
    id: 10,
    canExpand: true,
  },
  {
    name: 'Gingerbread',
    calories: 356,
    fat: 16.0,
    carbs: 49,
    protein: 3.9,
    sodium: 327,
    calcium: '7%',
    iron: '16%',
    id: 11,
    canExpand: false,
  },
  {
    name: 'Jelly bean',
    calories: 375,
    fat: 0.0,
    carbs: 94,
    protein: 0.0,
    sodium: 50,
    calcium: '0%',
    iron: '0%',
    id: 12,
    canExpand: false,
  },
  {
    name: 'Lollipop',
    calories: 392,
    fat: 0.2,
    carbs: 98,
    protein: 0,
    sodium: 38,
    calcium: '0%',
    iron: '2%',
    id: 13,
    canExpand: true,
  },
  {
    name: 'Honeycomb',
    calories: 408,
    fat: 3.2,
    carbs: 87,
    protein: 6.5,
    sodium: 562,
    calcium: '0%',
    iron: '45%',
    id: 14,
    canExpand: false,
  },
  {
    name: 'Donut',
    calories: 452,
    fat: 25.0,
    carbs: 51,
    protein: 4.9,
    sodium: 326,
    calcium: '2%',
    iron: '22%',
    id: 15,
    canExpand: false,
  },
  {
    name: 'KitKat',
    calories: 518,
    fat: 26.0,
    carbs: 65,
    protein: 7,
    sodium: 54,
    calcium: '12%',
    iron: '6%',
    id: 16,
    canExpand: false,
  }
]);

</script>
