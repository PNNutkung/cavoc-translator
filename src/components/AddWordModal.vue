<template>
  <modal :name="modalName">
    <form action="">
      <div class="add-new-word-modal">
        <h1>Add new word</h1>
        <h2 v-if="message !== ''">
          {{message}}
        </h2>
        <mu-text-field label="Japanese" name="japanese" labelFloat fullWidth />
        <mu-text-field label="Eniglish" name="english" labelFloat fullWidth />
        <mu-raised-button label="submit" primary fullWidth />
        <mu-raised-button label="cancel" fullWidth />
      </div>
    </form>
  </modal>
</template>

<script>
export default {
  data () {
    return {
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
    checkInputsData () {
      return false
    },
    addToDatabase () {
      if (this.checkInputsData()) {
        this.hide()
      } else {
        this.message = 'New words cannot be blank.'
      }
    },
    hide () {
      this.$modal.hide(this.modalName)
    }
  }
}
</script>

<style>
  .add-new-word-modal {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    height: 100%;
    padding: 20px;
  }
</style>
