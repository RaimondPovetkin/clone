<template>
  <div style="height: 100%;">
    <q-scroll-area style="width: 100%; height: 100%;">
      <div class="q-pa-md">
        <transition name="slide-fade">
          <div class="row justify-between" v-if="view == 'kanban'">
            <OrdersGrid :data="data"></OrdersGrid>
          </div>
          <div v-else>
            <OrdersTable></OrdersTable>
          </div>
        </transition>
      </div>
    </q-scroll-area>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import OrdersGrid from './OrdersGrid.vue';
import OrdersTable from './OrdersTable.vue';



const data = ([
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua., sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:1,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, ut labore et dolore magna aliqua.",
    id:2,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. incididunt ut labore et dolore magna aliqua.",
    id:3,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur ad, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.unt ut labore et dolore magna aliqua.",
    id:4,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit aagna aliqua.",
    id:5,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetincididu aliqua.",
    id:6,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur , sed do eiusmod tempor incid, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.idunt ut labore et dolore magna aliqua.adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:7,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adod tempor incididunt ut labore et dolore magna aliqua.",
    id:8,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:9,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:10,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur tempor incididunt ut labore et dolore magna aliqua.",
    id:11,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipisc, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.ing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:12,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consecte, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:13,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed or incididunt ut labore et dolore magna aliqua.",
    id:14,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:15,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sdidunt ut labore et dolore magna aliqua.",
    id:16,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit ut labore et dolore magna aliqua.",
    id:17,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do ei, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. ut labore et dolore magna aliqua.",
    id:18,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusdunt ut labore et dolore magna aliqua.",
    id:19,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:20,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:21,
    date: 42423432
  },
  {
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    id:22,
    date: 42423432
  },

])

const props = defineProps({
  view: {
    type: String,
    required: true,
    default: "kanban"
  },
})

</script>
<style lang="scss" scoped>
.q-scrollarea__container{
  min-height: 200px!important;
}
.my-card{
  width: 200px;
  height: 200px;
}

/* Анимации появления и исчезновения могут иметь */
/* различные продолжительности и динамику.       */
.slide-fade-enter-active {
  transition: all .6s ease;
}
.slide-fade-leave-active {
  transition: all .2s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateY(500px);
  opacity: 0;
}
</style>
