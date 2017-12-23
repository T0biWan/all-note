<template>
  <div id="app">
    <hero>all-note</hero> <!-- kommt später wahrschienlich weg !-->
  </div>
</template>

<script>
import hero from "./components/hero.vue"

export default {
  name: 'app',

  components: {
    'hero': hero,
  },
}
</script>

<style></style>
