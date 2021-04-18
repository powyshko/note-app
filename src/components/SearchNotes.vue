<template>
  <v-container>
    <v-row>
      <v-col>
        <v-text-field label="Search" outlined v-model="search"></v-text-field>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "SearchNotes",
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      search: this.value,
    };
  },
  watch: {
    search(value) {
      this.$emit("search", value);
    },
  },
};
</script>
