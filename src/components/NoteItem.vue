<template>
  <div class="noteBox">
    <div v-if="!note.editing">
      <div class="top">
        <button class="close" @click="removeNote">
          <img src="../assets/imgs/delete-2-svgrepo-com.svg" alt="Удалить" />
        </button>
        <button class="edit" @click="editNote">
          <img src="../assets/imgs/edit-3-svgrepo-com.svg" alt="Изменить" />
        </button>
      </div>
      <div :class="{'content': true, 'container-bold': note.isBold, 'container-italic': note.isItalic, 'container-underline': note.isUnderline, 'container-TNR': note.isTNR}" :style="{'font-size': note.fontSize + 'px'}">
        {{note.text}}
      </div>
      <button class="button-bold" @click="toggleBold">Ж</button>
      <button class="button-italic" @click="toggleItalic">К</button>
      <button class="button-underline" @click="toggleUnderline">П</button>
      <button class="button-TNR" @click="toggleTNR">TNR</button>
      <button class="button-increase-font" @click="increaseFontSize">+</button>
      <button class="button-decrease-font" @click="decreaseFontSize">-</button>
    </div>
    <div v-else>
      <div class="top">
        <button class="close" @click="removeNote">
          <img src="../assets/imgs/delete-2-svgrepo-com.svg" alt="Удалить" />
        </button>
        <button class="save" @click="saveNote">
          <img
            src="../assets/imgs/check-mark-circle-svgrepo-com.svg"
            alt="Сохранить"
          />
        </button>
        <button class="cancel" @click="cancelEdit">
          <img
            src="../assets/imgs/cross-circle-svgrepo-com.svg"
            alt="Отменить"
          />
        </button>
      </div>
      <textarea v-model="note.text" class="edit__input" v-on:keyup.enter="saveNote"></textarea>
    </div>
  </div>
</template>

<script>
export default {
  props: ["note"],
  methods: {
    removeNote() {
      this.$emit("remove-note");
    },
    editNote() {
      this.$emit("edit-note");
    },
    saveNote() {
      this.$emit("save-note");
    },
    cancelEdit() {
      this.$emit("cancel-edit");
    },
    toggleBold() {
      this.$emit("make-bold");
    },
    toggleItalic() {
      this.$emit("make-italic");
    },
    toggleUnderline() {
      this.$emit("make-underline");
    },
    decreaseFontSize() {
      this.$emit("make-smaller");
    },
    increaseFontSize() {
      this.$emit("make-bigger");
    },
    toggleTNR() {
      this.$emit("make-TNR");
    }
  },
};
</script>
