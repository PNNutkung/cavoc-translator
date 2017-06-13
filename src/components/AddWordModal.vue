<template>
  <div>
    <mu-flat-button label="Add new word" slot="right" @click="open"/>
    <mu-dialog :open="dialog" title="Add new word" @close="close">
      <form action="">
        <div class="add-new-word-modal">
          <h2 v-if="message !== ''">
            {{message}}
          </h2>
          <mu-text-field label="Japanese" name="japanese" labelFloat fullWidth />
          <mu-text-field label="Eniglish" name="english" labelFloat fullWidth />
          <mu-raised-button label="submit" primary fullWidth />
          <mu-raised-button id="cancel-modal-btn" label="cancel" fullWidth @click="close" />
        </div>
      </form>
    </mu-dialog>
  </div>
</template>

<script>
export default {
  name: 'add-word-modal',
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
      this.dialog = false
    },
    checkInputsData () {
      return false
    },
    addToDatabase () {
      if (this.checkInputsData()) {
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
