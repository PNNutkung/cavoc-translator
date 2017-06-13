<template>
  <div>
    <mu-flat-button label="Translate" @click="open" primary />
    <mu-dialog id="translate-dialog" title="Translate" :name="selectedWord.ja" :open="dialog" @close="close">
      <mu-table :showCheckbox="showCheckbox" :selectable="selectable">
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
      <div id="verify-div">
        <mu-checkbox label="Verify?" v-model="selectedWord.verified" id="modal-verify" name="word-verify" :value="selectedWord.verified"/>
      </div>
      <div id="modal-btns">
        <mu-flat-button label="G Translate" @click="googleTransalateAPIPost()" />
        <mu-flat-button label="Submit" @click="submit(selectedWord)" primary />
        <mu-flat-button label="Cancel" @click="cancel()" secondary />
      </div>
    </mu-dialog>
  </div>
</template>

<script>
import axios from 'axios'
import AUTH_TOKEN from '../config/translateAPI'

axios.defaults.headers.common['Authorization'] = `Bearer ${AUTH_TOKEN.key}`
axios.defaults.headers.post['Content-Type'] = 'application/json'

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
      axios.post(`https://translation.googleapis.com/language/translate/v2?q=${this.selectedWord.ja}&target=th&format=text&source=ja`)
      .then((res) => {
        this.selectedWord.th = res.data.data.translations[0].translatedText
      })
      .catch((err) => {
        console.log(err)
      })
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
    flex-direction: row;
    justify-content: space-around;
  }

  #translate-dialog {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }

  #verify-div {
    display: flex;
    justify-content: center;
    margin-top: 16px;
    margin-bottom: 16px;
  }

  td {
    white-space: normal;
    word-wrap: break-word;
  }
</style>
