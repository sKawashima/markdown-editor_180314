<template lang='pug'>
#app
  #editor(v-model='input')
  #preview(v-html='output')
</template>

<script>
import marked from 'marked'
import codemirror from 'codemirror'
import 'codemirror/lib/codemirror.css'

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
    codemirror(document.getElementById('editor'),{
      mode: 'markdown',
      lineNumbers: true,
      value: this.input
    })
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

#editor, #preview
  flex: 1 1 0
  overflow-y: scroll

#editor
  padding: 1em
  font-size: 12px
  background-color: #eee
  line-height: 1.5em
  font-family: 'Hack', courier, monospace
  border: 0

#preview
  padding: 1em

@media print
  #editor
    display: none
  #preview
    overflow-y: visible

</style>
