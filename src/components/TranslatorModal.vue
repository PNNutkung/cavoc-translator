<template>
  <modal name="word-check-modal" class="modal-for-translate">
    <div id="modal-content">
      <p id="translate-text">
        <h1>{{word.ja}}</h1>
        <h1>{{word.th}}</h1>
      </p>
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
  padding: 20px;
}
#modal-btns {
  display: flex;
  justify-content: space-around;
}
#translate-text {
  display: flex;
  justify-content: space-around;
  flex-direction: row;
}
</style>
