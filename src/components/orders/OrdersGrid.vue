<template>


  <div class="q-pa-md" style="width: 100%;">


    <div class="row">
      <div class="col"><q-card v-for="(item, index) in column1" :key="index">{{ item }}</q-card></div>
      <div class="col">.col</div>
      <div class="col"><q-card v-for="(item, index) in column2" :key="index">{{ item }}</q-card></div>
      <div class="col"><q-card v-for="(item, index) in column3" :key="index">{{ item }}</q-card></div>
    </div>



  </div>


</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';

const rows = ref([])

const deserts = ref([
  'Frozen Yogurtttttttttttttt tttttttttttttttttt ttttttt',
  'Ice cream sandwich',
  'Eclair',
  'Cupcake',
  'Gingerbread',
  'Jelly bean',
  'Lollipop',
  'Honeycomb',
  'Donut',
  'KitKat'
]);

//const rowsFinal = computed(() => props.todos.length);


onMounted(() => {
  console.log('33333')

  deserts.value.forEach(name => {
  for (let i = 0; i < 24; i++) {
    rows.value.push({ name: name + ' (' + i + ')', calories: 20 + Math.ceil(50 * Math.random()) })
  }
})

rows.value.sort(() => (-1 + Math.floor(3 * Math.random())))
})

const column1 = computed(() => {
  return rows.value.filter(i=>i.calories > 30)
});

const column2 = computed(() => {
  return rows.value.filter(i=>i.calories < 30)
});


const column3 = computed(() => {
  return rows.value.filter(i=>i.calories > 60)
});


</script>
<style lang="scss" >

</style>
