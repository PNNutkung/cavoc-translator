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
        <mu-tr v-for="word in words" :key="word.index">
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
               <mu-icon value="done" color="#4CAF50"/>
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
  props: ['wordsRef'],
  data () {
    return {
      showCheckbox: false,
      selectable: false,
      // TODO: Connect with Firebase.
      words: this.wordsRef
    }
  },
  methods: {
    show (word) {
      this.$modal.show(word.ja)
    },
    // TODO: save to Firebase
    editThaiTranslated (word) {
      console.log(word)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
