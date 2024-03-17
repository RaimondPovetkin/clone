<template>
<div>
  {{ rowItem }} <q-btn @click="addQuantity">+</q-btn>
</div>


</template>

<script setup lang="ts">
import { onMounted, ref,watch } from 'vue';
//import TableItem from 'src/components/table/TableItem.vue';

//const emit = defineEmits(['addItem','removeItem'])

const rowItem = ref(null)

const props = defineProps({
  row: {
    type: Object,
    required: false,
    default: ()=>{null}
  },
})


function addQuantity(){
  console.log(rowItem.value)
  rowItem.value.id = rowItem.value.id + 1
}


onMounted(() => {
  console.log(props)
  rowItem.value = props.row
})

</script>
<style lang="scss">
.tr-class{
  transition: all 1s;
}
</style>
