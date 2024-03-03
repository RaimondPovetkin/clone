<template>
  <div class="bg-white cursor-pointer" style="border-radius:50px; padding:6px" :style="outlined ? 'border: 1px solid'+ color : ''">
    <div class="selectorBlock" :style="'background-color:' + color" ref="selector"></div>
    <div ref="buttonsRow">
      <div v-if="labelIcons" style="line-height: 0px;" class="row buttonsRow justify-evenly">
        <div v-for="(item, index) in initionArr" :key="item.id">
          <div style="position: relative;" class="q-px-lg q-py-xs cursor-pointer item" @click="setBackground($event,item)" :class="selectedValue === item ? 'animBack' : 'animBackLast'">
            <div style="transition:all 0.5s" :class="selectedValue === item ? 'whiteFilter' : ''">
              <slot :name="'icon' + (index + 1)"></slot>
            </div>
          </div>
        </div>
      </div>
      <div v-else class="row buttonsRow justify-evenly">
        <div v-for="item in initionArr" :key="item.id" style="position: relative;" class="q-px-lg cursor-pointer item" @click="setBackground($event,item)" :class="selectedValue === item ? 'animBack' : 'animBackLast'">
          <div style="transition:all 0.5s" :class="selectedValue === item ? 'text-white' : ''" class="q-ma-sm">{{ item.label }}<q-badge v-if="item.badge" class="q-ml-sm" rounded align="middle" color="red" :label="item.badge" /></div>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref, computed, onMounted,watch } from "vue";
import { ButtonGroupItems } from '.././models';

const selector = ref(null);
const buttonsRow = ref(null);
const selectedValue = ref(null);
const sizeOffset = ref(0);
const currentColor = ref('#777777');

onMounted(() => {

  currentColor.value = props.color


  const currentId = props.initionArr.findIndex(i=>i.id == props.firstElement)


  let childrenItem = buttonsRow.value.children[0].children[currentId]

  selector.value.style.width = childrenItem.offsetWidth + 'px'
  selector.value.style.height = childrenItem.offsetHeight + 'px'
  selector.value.style.visibility = 'hidden'




  selectedValue.value = props.initionArr[currentId]
  sizeOffset.value = selector.value.getBoundingClientRect().left - buttonsRow.value.offsetLeft
  selector.value.style.left = childrenItem.getBoundingClientRect().left - sizeOffset.value + 'px';
})


const props = defineProps({
  firstElement: {
    type: Number,
    required: false,
    default: 1
  },
  initionArr: {
    type: Array,
    required: true
  },
  labelIcons: {
    type: Boolean,
    required: false,
    default: false
  },
  outlined: {
    type: Boolean,
    required: false,
    default: false
  },
  color: {
    type: String,
    required: false,
    default: "#302088"
  },
})


const emit = defineEmits(['select'])

function setBackground(el, name) {

  selector.value.style.visibility = 'visible'
  emit('select', name);
  selectedValue.value = name
  let targetElement = el.srcElement.closest(".item")

  selector.value.style.left = targetElement.getBoundingClientRect().left - sizeOffset.value + 'px';
  selector.value.style.width = targetElement.offsetWidth + 'px';
  selector.value.style.height = targetElement.offsetHeight + 'px';
  setTimeout(()=>{
    selector.value.style.visibility = 'hidden'
  }, 500);
}

</script>
<style lang="scss">

.selectorBlock{
    transition:all 0.5s ease;
    position:absolute;
    border-radius:50px;
}

.animBackLast{
    animation: background-fade2 .01s forwards;
}
@keyframes background-fade2 {
    0% {

        border-radius: 20px;
        background:#4E3BB0;
    }
    100% {
      background:none;
    }
}

.animBack{
    animation: background-fade .5s forwards;
    --colorFF1: #4E3BB0;
}
@keyframes background-fade {
    99.9% {
        background:none;
    }
    100% {
        border-radius: 20px;
        background-color: v-bind(currentColor);
    }
}

.whiteFilter{
  filter: brightness(0) saturate(100%) invert(100%) sepia(99%) saturate(17%) hue-rotate(340deg) brightness(104%) contrast(100%);
}
</style>
