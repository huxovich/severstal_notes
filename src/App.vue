<template>
  <div id="app">
    <note-input @add-note="addNote"></note-input>
    <h2 class="main__notes">📄 ваши заметки:</h2>
    <div class="notes-all">
      <note-item
        v-for="(note, index) in notes"
        :key="note.id"
        :note="note"
        @remove-note="removeNote(index)"
        @edit-note="editNote(index)"
        @make-bold="toggleBold(index)"
        @make-italic="toggleItalic(index)"
        @make-underline="toggleUnderline(index)"
        @save-note="saveNote(index)"
        @cancel-edit="cancelEdit(index)"
        @make-smaller="decreaseFontSize(index)"
        @make-bigger="increaseFontSize(index)"
        @make-TNR="toggleTNR(index)"
      >
      </note-item>
    </div>
  </div>
</template>

<script>
import NoteInput from "./components/NoteInput.vue";
import NoteItem from "./components/NoteItem.vue";

export default {
  components: {
    NoteInput,
    NoteItem,
  },
  data() {
    return {
      notes: [
        {
          text: "Первая заметка",
          editing: false,
          originalText: ""
        },
      ],
    };
  },
  mounted() {
    // Загрузка заметок из localStorage при монтировании компонента
    this.loadNotes();
  },
  methods: {
    addNote(text) {
       // Метод для добавления заметки
      this.notes.push({
        text,
        editing: false,
        originalText: "",
        fontSize: 20,
        fontStep: 2
      });
      this.saveNotes();
    },
    // Метод для удаления заметки
    removeNote(index) {
      this.notes.splice(index, 1);
      this.saveNotes();
    },
    // Метод для редактирования заметки
    editNote(index) {
      this.notes[index].editing = true;
      this.notes[index].originalText = this.notes[index].text;
    },
    // Метод для сохранения отредактированной заметки
    saveNote(index) {
      this.notes[index].editing = false;
      this.saveNotes();
    },
    // Метод для отмены редактирования заметки
    cancelEdit(index) {
      this.notes[index].editing = false;
      this.notes[index].text = this.notes[index].originalText;
    },
    // Метод для переключения жирного шрифта
    toggleBold(index) {
      const note = this.notes[index];
      if (note.isBold) {
        note.isBold = false;
        note.text = note.text.replace("container-bold", "");
      } else {
        note.isBold = true;
      }
      this.saveNotes();
    },
    // Метод для переключения курсивного шрифта
    toggleItalic(index) {
      const note = this.notes[index];
      if (note.isItalic) {
        note.isItalic = false;
        note.text = note.text.replace("container-italic", "");
      } else {
        note.isItalic = true;
      }
      this.saveNotes();
    },
    // Метод для переключения подчеркивания
    toggleUnderline(index) {
      const note = this.notes[index];
      if (note.isUnderline) {
        note.isUnderline = false;
        note.text = note.text.replace("container-underline", "");
      } else {
        note.isUnderline = true;
      }
      this.saveNotes();
    },
    // Метод для уменьшения размера шрифта
    decreaseFontSize(index){
      this.notes[index].fontSize -= this.notes[index].fontStep;
      this.saveNotes();
    },
    // Метод для увеличения размера шрифта
    increaseFontSize(index) {
      this.notes[index].fontSize += this.notes[index].fontStep;
      this.saveNotes();
    },
    // Метод для переключения шрифта Times New Roman
    toggleTNR(index) {
      const note = this.notes[index];
      if (note.isTNR) {
        note.isTNR = false;
        note.text = note.text.replace("container-TNR", "");
      } else {
        note.isTNR = true;
      }
      this.saveNotes();
    },
    // Метод для сохранения заметок в localStorage
    saveNotes() {
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },
    // Метод для загрузки заметок из localStorage
    loadNotes() {
      const savedNotes = localStorage.getItem("notes");
      if (savedNotes) {
        this.notes = JSON.parse(savedNotes);
      }
    }
  },
};
</script>

<style src='./assets/css/reset.css'></style>
<style src='./assets/css/style.css'></style>