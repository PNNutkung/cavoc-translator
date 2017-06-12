<template>
  <div class="translator-chart">
    <mu-table id="translating-table" :showCheckbox="showCheckbox" :selectable="selectable">
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
        <mu-th>
          <h2>Verified</h2>
        </mu-th>
        <mu-th>
          <h2>Translate</h2>
        </mu-th>
      </mu-thead>
      <mu-tbody>
        <mu-tr v-for="word in words" :key="word['.key']">
          <mu-td class="word-in-table">
            {{word.ja}}
          </mu-td>
          <mu-td class="word-in-table">
            {{word.en}}
          </mu-td>
          <mu-td class="word-in-table">
            {{word.th}}
          </mu-td>
          <mu-td>
            <h3 v-if="word.verified">
               <mu-icon value="done" :color="green"/>
            </h3>
          </mu-td>
          <mu-td>
            <mu-flat-button id="show-modal" label="Translate" class="demo-flat-button" primary @click="show(word)"/>
            <TranslatorModal :selectedWord="word" :edit-thai-translated="editThaiTranslated" />
          </mu-td>
        </mu-tr>
      </mu-tbody>
    </mu-table>
  </div>
</template>

<script>
import TranslatorModal from './TranslatorModal'
export default {
  name: 'translator-chart',
  components: {
    TranslatorModal
  },
  props: ['wordsFirebase', 'firebaseDb'],
  data () {
    return {
      showCheckbox: false,
      selectable: false,
      words: this.wordsFirebase,
      green: '#4CAF50'
    }
  },
  methods: {
    show (word) {
      this.$modal.show(word.ja)
    },
    editThaiTranslated (word) {
      let ref = this.firebaseDb.ref('words')
      ref.child(word['.key']).update({
        ja: word.ja,
        en: word.en,
        th: word.th,
        verified: word.verified
      })
    }
  }
}
</script>

<style scoped>
  td {
    white-space: normal;
    word-wrap: break-word;
  }
</style>
