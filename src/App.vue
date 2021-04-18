<template>
  <v-app class="wrapper">
    <v-main>
      <BaseH1>Notes App</BaseH1>
      <Message v-if="message" type="error">Fill in the title field</Message>
      <NewNote @addNote="addNote" />
      <SearchNotes :value="search" @search="search = $event" />
      <Notes :notes="notesFilters" />
    </v-main>
  </v-app>
</template>

<script>
import BaseH1 from "@/components/typography/BaseH1";
import NewNote from "@/components/NewNote";
import Notes from "@/components/Notes";
import Message from "@/components/Message";
import SearchNotes from "@/components/SearchNotes";

export default {
  name: "App",
  components: { BaseH1, NewNote, Notes, Message, SearchNotes },
  data() {
    return {
      notes: [
        {
          title: "Title first note",
          descr: "First note description",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standart",
        },
        {
          title: "Title middle note",
          descr: "Middle note description",
          date: new Date(Date.now()).toLocaleString(),
          priority: "High",
        },
        {
          title: "Title last note",
          descr: "Last note description",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Very High",
        },
      ],
      message: false,
      search: "",
    };
  },
  computed: {
    notesFilters() {
      let search = this.search.trim().toLowerCase();
      if (!search) return this.notes;

      let array = this.notes.filter((note) => {
        if (note.title.toLowerCase().indexOf(search) !== -1) {
          return note;
        }
      });

      return array;
    },
  },
  methods: {
    addNote(note) {
      let { title, descr, priority } = note;

      if (!title) {
        this.message = true;
        return;
      }

      const newNote = {
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
        priority,
      };

      this.notes.push(newNote);

      this.message = false;
      note.title = "";
      note.descr = "";
      note.priority = "Standart";
    },
  },
};
</script>

<style scoped>
.wrapper {
  width: 1040px;
  margin: 0 auto;
  padding: 40px 0px 0px 0px;
}
</style>
