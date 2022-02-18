<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Navigation
        </q-item-label>

        <Navigation
          v-for="link in navigationList"
          :key="link.title"
          v-bind="link"
          props=""
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Navigation from 'components/Navigation.vue'

const navigationList = [
  {
    title: 'Todo',
    caption: 'Todo list',
    icon: 'view_list',
    link: '/'
  },
  {
    title: 'Settings',
    caption: 'Change settings',
    icon: 'settings_input_component',
    link: '/settings'
  },

];

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    Navigation
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      navigationList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
