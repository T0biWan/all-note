<template>
  <div id="app">
    <hero title="all-note"></hero>  <!-- kommt später wahrschienlich weg !-->
    <textarea v-model="note_content"></textarea>
    <aside class="preview" v-html="render_note"></aside>
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
      note_content: localStorage.getItem('content') || 'Ph'nglui mglw'nafh Cthulhu R'lyeh wgah'nagl fhtagn.'
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
