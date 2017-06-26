<template>
  <div>
    <mu-flat-button label="Add new word" icon="add" @click="open"/>
    <mu-dialog :open="dialog" title="Add new word" @close="close">
      <form action="">
        <div class="add-new-word-modal">
          <h2 v-if="message !== ''">
            {{message}}
          </h2>
          <mu-text-field label="Japanese" name="japanese" v-model="newWords.ja" labelFloat fullWidth @keyup.native.enter="addToDatabase" />
          <mu-text-field label="English" name="english" v-model="newWords.en" labelFloat fullWidth @keyup.native.enter="addToDatabase" />
          <mu-raised-button label="submit" primary fullWidth @click="addToDatabase" />
          <mu-raised-button id="cancel-modal-btn" label="cancel" fullWidth @click="close" />
        </div>
      </form>
    </mu-dialog>
  </div>
</template>

<script>
export default {
  name: 'add-word-modal',
  props: ['firebaseDb'],
  data () {
    return {
      dialog: false,
      modalName: 'Add new word',
      newWords: {
        ja: '',
        en: '',
        th: '',
        verified: false
      },
      message: ''
    }
  },
  methods: {
    open () {
      this.dialog = true
    },
    close () {
      this.newWords = {
        ja: '',
        en: '',
        th: '',
        verified: false
      }
      this.message = ''
      this.dialog = false
    },
    checkInputsData () {
      return this.newWords.ja !== '' && this.newWords.en !== ''
    },
    addToDatabase () {
      if (this.checkInputsData()) {
        let ref = this.firebaseDb.ref('words')
        ref.push(this.newWords)
        this.close()
      } else {
        this.message = 'New words cannot be blank.'
      }
    }
  }
}
</script>

<style scoped>
  #cancel-modal-btn {
    margin-top: 10px;
  }
</style>
