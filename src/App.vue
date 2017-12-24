<template>
  <div id="app">
    <hero title="all-note"></hero>  <!-- kommt später wahrschienlich weg -->
    <aside></aside> <!-- display all notes -->
    <div> <!-- Toolbar -->
      <button @click="add_note">Add note</button>
    </div>
    <div> <!-- list of notes -->

    </div>
    <textarea v-model="note_content"></textarea>
    <aside v-html="render_note"></aside>
  </div>
</template>

<script>
import hero from "./components/hero.vue"

export default {
  name: 'app',

  components: {
    'hero': hero,
  },

  data() {
    return {
      note_content: localStorage.getItem('note_content') || "Ph'nglui mglw'nafh **Cthulhu** R'lyeh wgah'nagl fhtagn.",
      notes: [],
    };
  },

  computed: {
    render_note () {
      // return marked(this.note_content)
      return this.note_content
    },
  },

  methods: {
    save_note (val) {
      console.log('saving note:', val)
      localStorage.setItem('note_content', val)
    },

    add_note () {
      const time = Date.now()
      // Default new note
      const note = {
        id: String(time),
        title: 'New note ' + (this.notes.length + 1),
        note_content: '**Hi!** This notebook is using [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for formatting!',
        created: time,
        favorite: false,
      }
      // Add to the list
      this.notes.push(note)
    },
  },

  watch: {
    note_content: {
      handler: 'save_note',
      deep: true,
    },
  },
}
</script>

<style>
</style>
