<template>
<!-- app -->
<div id="app">
  <mu-flat-button id="show-modal" label="Translate" class="demo-flat-button" primary @click="translate(japaneseWord)"/>
  <!-- use the modal component, pass in the prop -->
  <modal v-if="showModal" @close="showModal = false">
    <!--
      you can use custom content here to overwrite
      default content
    -->
    <h3 slot="header">custom header</h3>
  </modal>
</div>
</template>

<script>
export default {
  name: 'modal',
  data () {
    return {
      showModal: false
    }
  },
  props: ['japaneseWord'],
  methods: {
    // TODO: Call tranlate API to Google Translate and show the translated back.
    translate (word) {
      this.showModal = true
      console.log(word)
      alert(`Hello ${word}`)
    }
  }
}
</script>

<style>

</style>
