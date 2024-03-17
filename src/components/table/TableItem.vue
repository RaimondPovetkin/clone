<template>

  <div v-for="(i, index) in copy" :key="index">
    <TableItemItem :row="i"></TableItemItem>
  </div>

</template>

<script setup lang="ts">
import { ref,watch } from 'vue';
import TableItemItem from 'src/components/table/TableItemItem.vue';

//const emit = defineEmits(['addItem','removeItem'])

const quantity = ref(null)
const copy = ref(null)

const props = defineProps({
  items: {
    type: Array,
    required: false,
    default: ()=>{[]}
  },
})


function addQuantity(){

}


watch(props, () => {
  console.log('watch')
  copy.value = props.items
})

</script>
<style lang="scss">
.tr-class{
  transition: all 1s;
}
</style>
