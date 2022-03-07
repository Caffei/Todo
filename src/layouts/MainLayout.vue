<template>
  <q-layout view="lhh lpR lFr">
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

        <q-toolbar-title class="absolute-center"> Multi </q-toolbar-title>
        <q-chip size="lg" color="secondary" class="absolute-right">
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
          </q-avatar>
          Naajak
        </q-chip>

        <div>Todo</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-primary"
    >
      <q-list dark>
        <q-item-label header> Navigation </q-item-label>

        <Navigation
          v-for="link in navigationList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Navigation from "components/Navigation.vue";

const navigationList = [
  {
    title: "Todo",
    caption: "Todo list",
    icon: "view_list",
    link: "/",
  },
  {
    title: "Memory",
    caption: "Memory",
    icon: "view_carousel",
    link: "/memory",
  },
  {
    title: "Settings",
    caption: "Change settings",
    icon: "settings",
    link: "/settings",
  },
];

import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  components: {
    Navigation,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      navigationList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
