<template>
  <transition-group
    appear
    enter-active-class="animated fadeIn"
    leave-active-class="animated fadeOut"
  >
    <!-- We wrap a "p" tag and a QBtn -->
    <p key="text">Lorem Ipsum</p>
    <q-btn key="email-button" color="secondary" icon="mail" label="Email" />
  </transition-group>
</template>

<script>
export default {
  data() {
    return {
      kwota: 0,
      kwota2: 0,
    };
  },
  methods: {
    losuj() {
      this.kwota = Math.random() * 3 + 1;
    },
  },
};
</script>

<style>
</style>
