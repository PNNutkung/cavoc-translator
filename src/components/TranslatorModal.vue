<template>
  <modal name="word-check-modal">
    <div slot="top-right">
      <button @click="hide()">
        ❌
      </button>
    </div>
    <div id="modal-content">
      {{word.ja}}
      <div id="modal-btns">
        <mu-flat-button label="G Translate" @click="googleTransalateAPIPost()" />
        <mu-flat-button label="Cancel" @click="hide()" secondary />
        <mu-flat-button label="Submit" @click="editThaiTranslated(word.ja)" primary />
      </div>
    </div>
  </modal>
</template>

<script>
export default {
  name: 'TranslatorModal',
  props: ['word', 'editThaiTranslated'],
  data () {
    return {
      wordToTranslate: this.word
    }
  },
  methods: {
    // TODO: Call tranlate API to Google Translate and show the translated back.
    googleTransalateAPIPost () {
      console.log(this.wordToTranslate.en)
    },
    hide () {
      this.$modal.hide('modal')
    }
  }
}
</script>

<style>
#modal-content {
  display: flex;
  flex-direction: column;
}
#modal-btns {
  display: flex;
  justify-content: space-around;
}
</style>
