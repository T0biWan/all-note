<template>
<div id="app">
  <hero title="all-note"></hero>
  <!-- kommt später wahrschienlich weg -->

  <div class="tile is-ancestor">
    <div class="tile is-parent is-vertical">
      <div class="tile is-child box">
        <button @click="addNote">Add note</button>
        <!-- <button @click="TODO">Delete note</button> -->
      </div>
      <div class="tile is-child box">
        <div v-for="note of notes" @click="selectNote(note)" :class="{ selected: note === selectedNote }">{{note.title}}</div>
      </div>
    </div>
    <div class="tile is-parent is-vertical is-9">
      <div class="tile is-child box">
        <button @click="toggleNotePreview">Render</button>
      </div>
      <div class="tile is-child box">
        <textarea v-if="isTextareVisible" v-model="selectedNote.content"></textarea>
        <div v-if="showNotePreview" v-html="notePreview"></div>
      </div>
    </div>
  </div>


</div>
</template>

<script>
import hero from "./components/hero.vue"
var marked = require('marked');

export default {
  name: 'app',

  components: {
    'hero': hero,
  },

  data() {
    return {
      // content: localStorage.getItem('content') || "Ph'nglui mglw'nafh **Cthulhu** R'lyeh wgah'nagl fhtagn.",
      notes: JSON.parse(localStorage.getItem('notes')) || [],
      // selected_note_id: null,
      selectedId: localStorage.getItem('selected-id') || null,
      showNotePreview: false,
    };
  },

  computed: {
    // render_note () {
    //   // return marked(this.content)
    //   return this.content
    // },
    //
    // selected_note () {
    //   return this.notes.find(note => note.id === this.selected_note_id)
    // },
    selectedNote() {
      // We return the matching note with selectedId
      return this.notes.find(note => note.id === this.selectedId)
    },

    notePreview() {
      // Markdown rendered to HTML
      return this.selectedNote ? marked(this.selectedNote.content) : ''
      // console.log(marked('I am using __markdown__.'));
      // return this.selectedNote.content;
      // return marked(this.selectedNote.content);
    },

    isTextareVisible() {
      return this.selectedNote && !this.showNotePreview;
    }
  },

  methods: {
    // save_note (val) {
    //   console.log('saving note:', val)
    //   localStorage.setItem('content', val)
    // },
    //
    // select_note_id (note) {
    //   this.selected_note = note.id
    // },
    //
    // add_note () {
    //   const time = Date.now()
    //   // Default new note
    //   const note = {
    //     id: String(time),
    //     title: 'New note ' + (this.notes.length + 1),
    //     content: '**Hi!** This notebook is using [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for formatting!',
    //     created: time,
    //     favorite: false,
    //   }
    //   // Add to the list
    //   this.notes.push(note)
    // },

    selectNote(note) {
      // This will update the 'selectedNote' computed property
      this.selectedId = note.id
    },

    // Add a note with some default content and select it
    addNote() {
      const time = Date.now()
      // Default new note
      const note = {
        id: String(time),
        title: 'New note ' + (this.notes.length + 1),
        content: "Ph'nglui mglw'nafh Cthulhu R'lyeh wgah'nagl fhtagn",
        created: time,
        favorite: false,
      }
      // Add
      this.notes.push(note)
      // Select
      this.selectNote(note)
    },

    saveNotes() {
      // Don't forget to stringify to JSON before storing
      localStorage.setItem('notes', JSON.stringify(this.notes))
      console.log('Notes saved!', new Date())
    },

    toggleNotePreview() {
      this.showNotePreview = !this.showNotePreview;
    },
  },

  watch: {
    // content: {
    //   handler: 'save_note',
    //   deep: true,
    // },
    // When our notes change, we save them
    notes: {
      // The method name
      handler: 'saveNotes',
      // We need this to watch each note's properties inside the array
      deep: true,
    },
    // Let's save the selection too
    selectedId(val, oldVal) {
      localStorage.setItem('selected-id', val)
    },
  },
}
</script>

<style>
.selected {
  background: #40b883;
  color: white;
}
</style>
