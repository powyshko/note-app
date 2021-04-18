<template>
  <v-alert outlined text :type="type">
    <slot></slot>
  </v-alert>
</template>

<script>
export default {
  name: "Message",
  props: {
    type: {
      type: String,
      default: "info",
    },
  },
};
</script>
