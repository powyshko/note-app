<template>
  <v-container class="note-body">
    <v-row>
      <v-col>
        <v-text-field label="Title" v-model="note.title"></v-text-field>
      </v-col>
      <v-col class="select-item">
        <v-select
          :items="itemsSelect"
          chips
          label="priority"
          v-model="note.priority"
        ></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-textarea solo label="Description" v-model="note.descr"></v-textarea>
      </v-col>
    </v-row>
    <v-btn depressed color="primary" @click="addNotes">
      New Note
    </v-btn>
  </v-container>
</template>

<script>
export default {
  name: "NewNote",
  data() {
    return {
      note: {
        title: "",
        descr: "",
        priority: "Standart",
      },
      itemsSelect: ["Standart", "High", "Very High"],
    };
  },
  methods: {
    addNotes() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>

<style scoped>
.note-body {
  text-align: center;
}

.select-item {
  padding: 2px 0px 0px 0px;
}
</style>
