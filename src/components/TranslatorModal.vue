<template>
  <div>
    <mu-flat-button label="Translate" @click="open" primary />
    <mu-dialog title="Translate" :name="selectedWord.ja" :open="dialog" @close="close">
      <mu-table id="translating-modal" :showCheckbox="showCheckbox" :selectable="selectable">
        <mu-thead>
          <mu-th>
            <h2>Japanese</h2>
          </mu-th>
          <mu-th>
            <h2>English</h2>
          </mu-th>
          <mu-th>
            <h2>Thai</h2>
          </mu-th>
        </mu-thead>
        <mu-tbody>
          <mu-tr>
            <mu-td>
              {{selectedWord.ja}}
            </mu-td>
            <mu-td>
              {{selectedWord.en}}
            </mu-td>
            <mu-td>
              <mu-text-field hintText="Thai" v-model="selectedWord.th" :value="selectedWord.th" fullWidth />
            </mu-td>
          </mu-tr>
        </mu-tbody>
      </mu-table>
      <mu-checkbox label="Verify?" v-model="selectedWord.verified" id="modal-verify" name="word-verify" :value="selectedWord.verified"/>
      <div id="modal-btns">
        <mu-flat-button label="G Translate" @click="googleTransalateAPIPost()" />
        <mu-flat-button label="Cancel" @click="cancel()" secondary />
        <mu-flat-button label="Submit" @click="submit(selectedWord)" primary />
      </div>
    </mu-dialog>
  </div>
</template>

<script>
export default {
  name: 'TranslatorModal',
  props: ['selectedWord', 'editThaiTranslated'],
  data () {
    return {
      showCheckbox: false,
      selectable: false,
      defaultThWord: '',
      defaultVerified: null,
      dialog: false
    }
  },
  methods: {
    // TODO: Call tranlate API to Google Translate and show the translated back.
    googleTransalateAPIPost () {
      console.log(this.selectedWord.ja)
    },
    cancel () {
      this.selectedWord.th = this.defaultThWord
      this.selectedWord.verified = this.defaultVerified
      this.close()
    },
    close () {
      this.dialog = false
    },
    submit (word) {
      this.editThaiTranslated(word)
      this.close()
    },
    open () {
      this.dialog = true
      this.defaultThWord = this.selectedWord.th
      this.defaultVerified = this.selectedWord.verified
    }
  }
}
</script>

<style scoped>
  #modal-btns {
    display: flex;
    justify-content: space-around;
  }

  #modal-verify {
    display: flex;
    justify-content: center;
  }

  td {
    white-space: normal;
    word-wrap: break-word;
  }
</style>
