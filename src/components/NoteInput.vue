<template>
  <div>
    <h1 class="main__title">заметки</h1>
    <textarea
      placeholder="Что тебе напомнить?"
      v-model="note.text"
      v-on:keyup.enter="addNote"
      class="main__input"
    ></textarea>
    <button class="main__button" @click="addNote">Добавить запись</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      note: {
        text: "",
        editing: false,
        originalText: "",
        isBold: false,
        isItalic: false,
        isInderline: false,
        isTNR: false,
        fontSize: 16,
        fontStep: 2
      },
    };
  },
  methods: {
    addNote() {
      let { text } = this.note;
      if (text.trim() === "") {
        return;
      }
      this.$emit("add-note", text);
      this.note.text = "";
    },
  },
};
</script>
