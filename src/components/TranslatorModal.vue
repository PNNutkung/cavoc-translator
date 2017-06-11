<template>
  <modal name="word-check-modal" @before-open="beforeOpen">
    <div id="modal-content">
      <mu-table id="translating-modal" :showCheckbox="showCheckbox" :selectable="selectable">
        <mu-tbody>
          <mu-tr>
            <mu-td>
              {{word.ja}}
            </mu-td>
            <mu-td>
              {{word.en}}
            </mu-td>
            <mu-td>
              <input type="text" name="thai-lang" v-model="word.th" :value="word.th">
            </mu-td>
          </mu-tr>
        </mu-tbody>
      </mu-table>
      <span>
        <input type="checkbox" v-model="word.verified" id="modal-checkbox" name="word-verify" :value="word.verified"/>
        <label for="modal-checkbox">Verify?</label>
      </span>
      <div id="modal-btns">
        <mu-flat-button label="G Translate" @click="googleTransalateAPIPost()" />
        <mu-flat-button label="Cancel" @click="cancel()" secondary />
        <mu-flat-button label="Submit" @click="submit(word)" primary />
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
      showCheckbox: false,
      selectable: false,
      defaultThWord: '',
      defaultVerified: null
    }
  },
  methods: {
    // TODO: Call tranlate API to Google Translate and show the translated back.
    googleTransalateAPIPost () {
      console.log(this.word.ja)
    },
    cancel () {
      this.word.th = this.defaultThWord
      this.word.verified = this.defaultVerified
      this.hide()
    },
    hide () {
      this.$modal.hide('word-check-modal')
    },
    submit (word) {
      // TODO: Save to Firebase.
      this.editThaiTranslated(word)
      this.hide()
    },
    beforeOpen (event) {
      this.defaultThWord = this.word.th
      this.defaultVerified = this.word.verified
    }
  }
}
</script>

<style scoped>
  #modal-content {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 20px;
  }

  #modal-btns {
    display: flex;
    justify-content: space-around;
  }
</style>
