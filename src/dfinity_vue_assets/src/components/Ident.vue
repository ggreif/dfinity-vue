<template>
  <v-btn v-if="connected" @click="toggle">
    <span>Sign Out</span>
    <v-icon right>logout</v-icon>
  </v-btn>
  <v-btn v-else @click="toggle">
    <span>Sign In</span>
    <v-icon right>login</v-icon>
  </v-btn>
</template>

<script>
export default {
  data: () => {
    return { connected: false }
  },
  methods: {
    toggle() { this.connected = !this.connected }
  }
};
</script>
