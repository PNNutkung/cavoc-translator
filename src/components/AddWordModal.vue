<template>
  <modal :name="modalName">
    <h2 v-if="message !=== ''">
      {{message}}
    </h2>
    <form action="">
      <div class="add-new-word-modal">
        <mu-text-field label="Japanese" name="japanese" labelFloat />
        <mu-text-field label="Eniglish" name="english" labelFloat />
      </div>
      <mu-raised-button label="submit" fullWidth/>
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

</style>
