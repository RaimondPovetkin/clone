<template>
  <q-page :style-fn="()=>{}">
    <div>
      ChatsPage


    <div class="flex q-mx-lg">
      <q-input class="q-mx-lg q-my-sm" style="width: 300px" filled label="Filled" />
      <q-input class="q-mx-lg q-my-sm" style="width: 300px" filled label="Filled" />
      <q-input class="q-mx-lg q-my-sm" style="width: 300px" filled label="Filled" />
      <q-input class="q-mx-lg q-my-sm" style="width: 300px" filled label="Filled" />
      <q-input class="q-mx-lg q-my-sm" style="width: 300px" filled label="Filled" />
    </div>
    <!-- <pre>
      {{ simple }}
    </pre> -->

    <q-tree
      :nodes="simple"
      node-key="label"
      no-connectors
    >
      <template v-slot:default-header="prop">
        <div class="row q-gutter-x-md"
            :style="{width: '100%', pointerEvents: prop.node.delete ? 'none' : 'auto'}"
            :disabled="prop.node.delete"
        >
          <div class="col" style="width: 150px">
            <span>{{ prop.node.label }} / {{ prop.node.label }}</span>
          </div>

          <div class="col">
            555
          </div>

        </div>
      </template>
    </q-tree>

    {{ actives }}


    <div class="container">
      <div class="progress-container">
        <div class="progress" :style="'width:' + widthBar + '%'" id="progress"></div>

        <div class="circle" :class="actives.find(item=>item === i) ? 'active' : ''" v-for="(i,index) in circles" :key="i">{{i}}</div>


      </div>
    </div>

    <q-btn @click="prev">назад</q-btn>
    <q-btn @click="next">вперёд</q-btn>


    </div>
  </q-page>
</template>

<script setup lang="ts">
import { I } from 'app/dist/spa/assets/index.a824162d';
import { ref, computed } from 'vue';

function prev(){
  actives.value.splice(actives.value.length - 1,1)
}

const widthBar = computed(() => {
  return (actives.value.length - 1) / (circles.value.length - 1) * 100
});

function next(){
  if(!actives.value.length){
    actives.value.push(1)
  } else if(actives.value.length === circles.value.length) {
    return
  } else{
    actives.value.push(actives.value[actives.value.length-1] + 1)
  }

}

//const widthBar = ref(0)

const actives = ref([1,2,3])

const circles = ref([1,2,3,4])

const simple = ref([
        {
          label: 'Satisfied customers (with avatar)',
          avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
          children: [
            {
              label: 'Good food (with icon)',
              icon: 'restaurant_menu',
              children: [
                { label: 'Quality ingredients' },
                { label: 'Good recipe' }
              ]
            },
            {
              label: 'Good service (disabled node with icon)',
              icon: 'room_service',
              disabled: true,
              children: [
                { label: 'Prompt attention' },
                { label: 'Professional waiter' }
              ]
            },
            {
              label: 'Pleasant surroundings (with icon)',
              icon: 'photo',
              children: [
                {
                  label: 'Happy atmosphere (with image)',
                  img: 'https://cdn.quasar.dev/img/logo_calendar_128px.png'
                },
                { label: 'Good table presentation' },
                { label: 'Pleasing decor' }
              ]
            }
          ]
        },
        {
          label: 'Satisfied customers (with avatar)2',
          avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
          children: [
            {
              label: 'Good food (with icon)2',
              icon: 'restaurant_menu',
              children: [
                { label: 'Quality ingredients2' },
                { label: 'Good recipe2' }
              ]
            },
            {
              label: 'Good service (disabled node with icon)2',
              icon: 'room_service',
              disabled: true,
              children: [
                { label: 'Prompt attention2' },
                { label: 'Professional waiter2' }
              ]
            },
            {
              label: 'Pleasant surroundings (with icon)2',
              icon: 'photo',
              children: [
                {
                  label: 'Happy atmosphere (with image)2',
                  img: 'https://cdn.quasar.dev/img/logo_calendar_128px.png'
                },
                { label: 'Good table presentation2' },
                { label: 'Pleasing decor2' }
              ]
            }
          ]
        }
      ])

</script>
<style scoped>

:root {
--line-border-fill: #3498db;
--line-border-empty: #e0e0e0;
}
* {
box-sizing: border-box;
}
body {
background-color: #f6f7fb;
font-family: 'Muli', sans-serif;
display: flex;
align-items: center;
justify-content: center;
height: 100vh;
overflow: hidden;
margin: 0;
}
.container {
text-align: center;
}
.progress-container {
display: flex;
justify-content: space-between;
position: relative;
margin-bottom: 30px;
max-width: 100%;
width: 350px;
}
.progress-container::before {
content: '';
background-color: var(--line-border-empty);
position: absolute;
top: 50%;
left: 0;
transform: translateY(-50%);
height: 4px;
width: 100%;
z-index: -1;
}
.progress {
background-color: red;
position: absolute;
top: 50%;
left: 0;
transform: translateY(-50%);
height: 4px;
width: 0%;
transition: 0.4s ease;
}
.circle {
position: relative;
background-color: #fff;
color: #999;
border-radius: 50%;
height: 30px;
width: 30px;
display: flex;
align-items: center;
justify-content: center;
border: 3px solid var(--line-border-empty);
transition: 0.4s ease;
}
.circle.active {
background-color: red
}
.btn {
background-color: var(--line-border-fill);
color: #fff;
border: 0;
border-radius: 6px;
cursor: pointer;
font-family: inherit;
padding: 8px 30px;
margin: 5px;
font-size: 14px;
}
.btn:active {
transform: scale(0.98);
}
.btn:focus {
outline: 0;
}
.btn:disabled {
background-color: var(--line-border-empty);
cursor: not-allowed;
}

</style>
