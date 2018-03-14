<template lang='pug'>
#app
  textarea.markdown(v-model='input')
  #preview(v-html='output')
</template>

<script>
import marked from 'marked'
import highlight from'highlight.js'
import 'highlight.js/styles/atom-one-dark.css'

export default {
  name: 'app',
  data () {
    return {
      input: localStorage.getItem('markdown-editor_180314'),
      output: ''
    }
  },
  watch: {
    input: function () {
      this.output = marked(this.input)
      localStorage.setItem('markdown-editor_180314', this.input)
    }
  },
  mounted () {
    this.output = marked(this.input)
    highlight.initHighlightingOnLoad()
    console.log(highlight)
  }
}
</script>

<style lang='sass'>
html, body
  height: 100%
  width: 100%
  margin: 0

#app
  display: flex
  height: 100%

textarea, #preview
  flex: 1 1 0
  overflow-y: scroll

textarea
  padding: 1em
  font-size: 12px
  background-color: #eee
  line-height: 1.5em
  font-family: 'Hack', courier, monospace
  border: 0

#preview
  padding: 1em

@media print
  textarea
    display: none
  #preview
    overflow-y: visible

</style>
