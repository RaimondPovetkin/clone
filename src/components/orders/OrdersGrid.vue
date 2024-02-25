<template>


<div class="q-pa-md" style="width: 100%;">
    <q-table
      grid
      :card-container-class="cardContainerClass"
      title="Treats"
      :rows="rows"
      :columns="columns"
      row-key="name"
      hide-header
      v-model:pagination="pagination"
      :rows-per-page-options="rowsPerPageOptions"
      :hide-pagination= "true"

    >
      <template v-slot:item="props">
        <div class="q-pa-xs col-xs-12 col-sm-6 col-md-4">
          <q-card>
            <q-card-section class="text-center">
              Calories for
              <br>
              <strong>{{ props.row.name }}</strong>
            </q-card-section>
            <q-separator></q-separator>
            <q-card-section class="flex flex-center" :style="{ fontSize: props.row.calories + 'px' }">
              <div>{{ props.row.calories }} g</div>
            </q-card-section>
          </q-card>
        </div>
      </template>
    </q-table>
  </div>


</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { useQuasar } from 'quasar'

const deserts = ref([
  'Frozen Yogurt',
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
const $q = useQuasar()

const cardContainerClass = computed(() => {
        return $q.screen.gt.xs
          ? 'grid-masonry grid-masonry--' + ($q.screen.gt.sm ? '3' : '2')
          : null
      });


const rowsPerPageOptions = computed(() => {
  return $q.screen.gt.xs
          ? $q.screen.gt.sm ? [ 240, 6, 9 ] : [ 240, 6 ]
          : [240]


})


function getItemsPerPage () {
      if ($q.screen.lt.sm) {
        return 3
      }
      if ($q.screen.lt.md) {
        return 6
      }
      return 240
    }

const rows = ref([])


const pagination = ref({
      page: 1,
      rowsPerPage: getItemsPerPage()
    })



const columns = ref([
        { name: 'name', label: 'Name', field: 'name' },
        { name: 'calories', label: 'Calories (g)', field: 'calories' }
      ],)


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


const props = defineProps({
  data: {
    type: Array,
    required: true,
    default: []
  },
})

</script>
<style lang="scss" >

.grid-masonry {
  flex-direction: column;
  height: 16000px;
}
.grid-masonry--2 > div:nth-child(2n+1) {
  order: 1;
}
.grid-masonry--2 > div:nth-child(2n) {
  order: 2;
}
.grid-masonry--2:before {
  content: "";
  flex: 1 0 100% !important;
  width: 0 !important;
  order: 1;
}
.grid-masonry--3 > div:nth-child(3n+1) {
  order: 1;
}
.grid-masonry--3 > div:nth-child(3n+2) {
  order: 2;
}
.grid-masonry--3 > div:nth-child(3n) {
  order: 3;
}
.grid-masonry--3:before, .grid-masonry--3:after {
  content: "";
  flex: 1 0 100% !important;
  width: 0 !important;
  order: 2;
}
</style>
