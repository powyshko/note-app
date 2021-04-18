<template>
  <v-col md="6" class="item-note">
    <v-card elevation="2" outlined :class="noteColorsPriority">
      <v-card-title class="item-title" @click="editFieldTitle(data.title)">
        {{ data.title }}
        <v-text-field
          class="item-title-edit"
          v-model="editTitle"
          solo
          clearable
          v-if="editTitle"
          @keyup.enter="setEditTitle"
        ></v-text-field>
      </v-card-title>
      <v-card-text class="item-descr" @click="editFieldDescr(data.descr)">
        {{ data.descr }}
        <v-textarea
          solo
          label="Description"
          v-model="editDesc"
          class="item-descr-edit"
          height="100px"
          v-if="editDesc"
          @keyup.enter="setEditDescr"
          clearable
        ></v-textarea>
      </v-card-text>
      <v-card-subtitle>
        {{ data.date }}
      </v-card-subtitle>
      <v-card-actions class="d-flex justify-end">
        <v-btn color="primary" text @click="removeNote(index)">
          Delete
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-col>
</template>

<script>
export default {
  name: "SingleNote",
  props: {
    data: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      editTitle: "",
      editDesc: "",
    };
  },
  computed: {
    noteColorsPriority() {
      return this.data.priority
        .split(" ")
        .join("")
        .toLowerCase();
    },
  },
  methods: {
    removeNote(index) {
      let isConfirm = confirm("Do you want to delete a note?");
      if (!isConfirm) return;
      this.$emit("remove", index);
    },
    editFieldTitle(title) {
      this.editTitle = title;
    },
    editFieldDescr(descr) {
      this.editDesc = descr;
    },
    setEditTitle() {
      this.data.title = this.editTitle;
      this.data.date = new Date(Date.now()).toLocaleString();
      this.editTitle = "";
    },
    setEditDescr() {
      this.data.descr = this.editDesc;
      this.data.date = new Date(Date.now()).toLocaleString();
      this.editDesc = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.item-note {
  transition: all 0.3s ease;
}

.standart {
  border: 2px solid #1de9b6;
}
.high {
  border: 2px solid #ef9a9a;
}
.veryhigh {
  border: 2px solid #b71c1c;
}

.item-title,
.item-descr {
  position: relative;
}

.item-title-edit {
  position: absolute;
  top: 16px;
  left: 16px;
  z-index: 10;
}

.item-descr-edit {
  position: absolute;
  top: 0px;
  left: 16px;
  z-index: 10;
}
</style>
