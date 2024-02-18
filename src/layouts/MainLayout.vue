<template>
  <q-layout view="lHr LpR lFr">
    <header style="height: 175px;" class="bg-primary">
      <div class="lllh">
        <q-toolbar class="row justify-between">
          <div>
            <img
              src="../assets/icons/logoSPPL.svg"
              alt="logo"
              height="25px"
              width="116px" />
          </div>
          <ButtonToggleVue
            color="#302088"
            :initionArr="menuItems"
            @select="selectPage"
          ></ButtonToggleVue>
          <div class="row items-center">
            <div class="q-mr-xl">
              <div class="text-body1 text-white">
                Иванов А. Е.
              </div>
              <div class="text-caption text-white">
                Специалист
              </div>
            </div>
            <div>
              <q-btn
                padding="sm"
                color="white"
                dark-percentage
                style="color:#424144 !important"
              >
              <img
                src="../assets/icons/logout.svg"
                height="15px"
                width="15px" />
              </q-btn>
            </div>
          </div>
        </q-toolbar>
      </div>
    </header>

    <q-dialog v-model="dialog" full-height position="right">
      <q-card style="width: 50vw; height: 100vh;">
        <q-linear-progress :value="0.6" color="pink" />

        <q-card-section class="row items-center no-wrap">
          <div>
            <div class="text-weight-bold">The Walker</div>
            <div class="text-grey">Fitz & The Tantrums</div>
          </div>

          <q-space />

          <q-btn flat round icon="fast_rewind" />
          <q-btn flat round icon="pause" />
          <q-btn flat round icon="fast_forward" />
        </q-card-section>
      </q-card>
    </q-dialog>

    <div style="position: fixed;height: calc(100% - 110px - 24px);width: 100vw;top: 110px;">
      <div style="display: grid; height: 100%;">
        <div class="q-mx-lg bg-white" style="border-radius: 16px; ">
            <!-- <q-btn
                flat
                dense
                round
                icon="menu"
                aria-label="Menu"
                @click="dialog = true"
            /> -->

            <q-page-container style="height: 100%; width: 100%;">
              <router-view />
            </q-page-container>

        </div>
      </div>
    </div>

  </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
//import EssentialLink, { EssentialLinkProps } from 'components/EssentialLink.vue';
import ButtonToggleVue from '../components/UI/ButtonToggle.vue';
import {useRouter} from 'vue-router'

// const essentialLinks: EssentialLinkProps[] = [
//   {
//     title: 'Docs',
//     caption: 'quasar.dev',
//     icon: 'school',
//     link: 'https://quasar.dev'
//   },
//   {
//     title: 'Github',
//     caption: 'github.com/quasarframework',
//     icon: 'code',
//     link: 'https://github.com/quasarframework'
//   },
//   {
//     title: 'Discord Chat Channel',
//     caption: 'chat.quasar.dev',
//     icon: 'chat',
//     link: 'https://chat.quasar.dev'
//   },
//   {
//     title: 'Forum',
//     caption: 'forum.quasar.dev',
//     icon: 'record_voice_over',
//     link: 'https://forum.quasar.dev'
//   },
//   {
//     title: 'Twitter',
//     caption: '@quasarframework',
//     icon: 'rss_feed',
//     link: 'https://twitter.quasar.dev'
//   },
//   {
//     title: 'Facebook',
//     caption: '@QuasarFramework',
//     icon: 'public',
//     link: 'https://facebook.quasar.dev'
//   },
//   {
//     title: 'Quasar Awesome',
//     caption: 'Community Quasar projects',
//     icon: 'favorite',
//     link: 'https://awesome.quasar.dev'
//   }
// ];

const leftDrawerOpen = ref(false)
const dialog = ref(false)
const menuItems = ref([
  {
    label:'Заявки',
    badge: null,
    path:'orders',
    id:1
  },
  {
    label:'Черновики',
    badge: null,
    path:'drafts',
    id:2
  },
  {
    label:'Чаты',
    badge: 1,
    path:'chats',
    id:3
  },
])

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

const router = useRouter();

function selectPage(el) {
  router.push({ path: el.path })
}

</script>
<style lang="scss" scoped>
.q-toolbar{
  padding: 31px;
}
.lllh{
  background-image: url("../assets/images/headerBackground.png");
  height: 100%;
}
</style>
