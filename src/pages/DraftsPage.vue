<template>
    <div class="flex justify-between">
        <div><pre>{{ items }}</pre></div>
        <div><q-btn @click="prepare(items)">PREPARE</q-btn></div>
        <div><pre>{{ result }}</pre></div>
    </div>


</template>

<script setup lang="ts">
import { ref } from 'vue';
//import TableItem from 'src/components/table/TableItem.vue';

const result = ref([])


function findUnselected(array){
    for (let index = 0; index < array.length; index++) {
    const element = array[index];
    if (element.selected === false) {
      return element;
    } else {
      if (element.children) {
        const found = findUnselected(element.children);
        if (found) {
          return found;
        }
      }
    }
  }
}

function prepare(items){
    items.forEach(el=>{
        if(el.selected){
            result.value.push(el)
        }
        if(el.selected === null){
            if(!findUnselected(el.children)){
                result.value.push(el)
            } else {
                prepare(el.children)
            }
        }
    })

}

const items = ref([
  {
    id:1,
    selected: true,
  },
  {
    id:2,
    selected: null,
    children:[
        {
            id:3,
            selected: false,
        },
        {
            id:4,
            selected: null,
            children:[
            {
                id:6,
                selected: true,
            },
            {
                id:7,
                selected: null,
                children:[
                {
                    id:8,
                    selected: true,
                },
                {
                    id:9,
                    selected: true,
                },
                ]
            },


            {
                id:33,
                selected: null,
                children:[
                {
                    id:12,
                    selected: false,
                },
                {
                    id:13,
                    selected: true,
                },
                ]
            },


            ]
        },
    ]
  },
  {
    id:5,
    selected: true,
  },
])

</script>
