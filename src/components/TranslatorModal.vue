<template>
  <modal :name="selectedWord.ja" @before-open="beforeOpen">
    <div id="modal-content">
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
              <input type="text" name="thai-lang" v-model="selectedWord.th" :value="selectedWord.th">
            </mu-td>
          </mu-tr>
        </mu-tbody>
      </mu-table>
      <span class="verified-checkbox">
        <mu-checkbox label="Verify?" v-model="selectedWord.verified" id="modal-checkbox" name="word-verify" :value="selectedWord.verified"/>
      </span>
      <div id="modal-btns">
        <mu-flat-button label="G Translate" @click="googleTransalateAPIPost()" />
        <mu-flat-button label="Cancel" @click="cancel()" secondary />
        <mu-flat-button label="Submit" @click="submit(selectedWord)" primary />
      </div>
    </div>
  </modal>
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
      defaultVerified: null
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
      this.hide()
    },
    hide () {
      this.$modal.hide(this.selectedWord.ja)
    },
    submit (word) {
      this.editThaiTranslated(word)
      this.hide()
    },
    beforeOpen (event) {
      this.defaultThWord = this.selectedWord.th
      this.defaultVerified = this.selectedWord.verified
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
    height: 100%;
  }

  #modal-btns {
    display: flex;
    justify-content: space-around;
  }

  .verified-checkbox {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }

  td {
    white-space: normal;
    word-wrap: break-word;
  }
</style>
