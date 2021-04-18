<template>
  <v-container class="body-notes">
    <v-row class="d-flex justify-space-between">
      <v-col><BaseH1 class="title-notes">Notes</BaseH1></v-col>
      <v-col class="icons">
        <IconGrid
          class="icon-item"
          :class="{ active: grid }"
          @click="grid = true"
        />
        <IconColumn
          class="icon-item"
          :class="{ active: !grid }"
          @click="grid = false"
        />
      </v-col>
    </v-row>
    <v-row>
      <template v-if="notes.length">
        <SingleNote
          v-for="(note, index) in notes"
          :key="`note-${index}`"
          :data="note"
          :index="index"
          @remove="removeNote"
          :class="{ active: grid }"
        />
      </template>
      <template v-else>
        <Message>Notes is empty</Message>
      </template>
    </v-row>
  </v-container>
</template>

<script>
import SingleNote from "./SingleNote";
import BaseH1 from "@/components/typography/BaseH1";
import IconGrid from "@/assets/icons/grid.svg";
import IconColumn from "@/assets/icons/column.svg";
import Message from "@/components/Message";

export default {
  name: "Notes",
  components: { SingleNote, BaseH1, IconGrid, IconColumn, Message },
  props: {
    notes: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      grid: false,
    };
  },
  methods: {
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style lang="scss" scoped>
.body-notes {
  margin: 20px 0px;
}

.title-notes {
  margin: 0px 0px 10px 0px;
}

.icons {
  text-align: right;
}

.icon-item {
  cursor: pointer;
  margin: 0px 5px 0px 0px;

  &.active {
    color: #1a237e;
  }

  &:last-child {
    margin: 0;
  }
}

.active {
  transition: all 0.3s ease;
  flex: 0 0 100% !important;
  max-width: 100% !important;
}
</style>
