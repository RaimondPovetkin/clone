<template>
  <q-page style="height: 100%;" :style-fn="()=>{}">



    <div style="display: grid;height: 100%; grid-template-rows: 90px auto">
      <div class="row justify-between items-center q-pa-lg">
        <div class="text-h5">Заявки</div>
        <div>
            <button-toggle
                :initionArr="viewItems"
                @select="selectPage"
                outlined
                labelIcons
                color="#4E3BB0"
            >
                <template v-slot:icon1>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M9 5V9H21V5M9 19H21V15H9M9 14H21V10H9M4 9H8V5H4M4 19H8V15H4M4 14H8V10H4V14Z" fill="#4E3BB0"/>
                  </svg>
                </template>
                <template v-slot:icon2>
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M16 20H20V16H16M16 14H20V10H16M10 8H14V4H10M16 8H20V4H16M10 14H14V10H10M4 14H8V10H4M4 20H8V16H4M10 20H14V16H10M4 8H8V4H4V8Z" fill="#4E3BB0"/>
                  </svg>
                </template>

            </button-toggle>
        </div>
      </div>
      <div class="q-mx-lg" style="background-color: #F5F5F6;display: grid;height: 100%; grid-template-rows: 50px auto; border-radius: 8px 8px 0 0;">
        <orders-controller></orders-controller>
        <orders-list :view="currentView"></orders-list>
      </div>
    </div>


  </q-page>
</template>

<script setup lang="ts">
import OrdersController from 'src/components/orders/OrdersController.vue';
import OrdersList from 'src/components/orders/OrdersList.vue';
import ButtonToggle from 'src/components/UI/ButtonToggle.vue';
import { ref } from 'vue';

function selectPage(el) {
  currentView.value = el.name
}
const currentView = ref('kanban')
const viewItems = ref([
  {
    badge: null,
    name: 'kanban',
    id:1
  },
  {
    badge: null,
    name: 'table',
    id:2
  }
])
</script>
