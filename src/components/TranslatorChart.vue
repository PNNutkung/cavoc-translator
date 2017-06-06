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
          <mu-td>
            {{word.ja}}
          </mu-td>
          <mu-td>
            {{word.en}}
          </mu-td>
          <mu-td>
            {{word.th}}
          </mu-td>
          <mu-td>
            <h3 v-if="word.verified">
               <mu-icon value="done" color="#4CAF50"/>
            </h3>
          </mu-td>
          <mu-td>
             <mu-flat-button label="Translate" class="demo-flat-button" primary @click="translate(word.ja)"/>
          </mu-td>
        </mu-tr>
      </mu-tbody>
    </mu-table>
  </div>
</template>

<script>
export default {
  name: 'translator-chart',
  data () {
    return {
      showCheckbox: false,
      selectable: false,
      words: [{
        ja: '農作業',
        en: 'Agriculture activity',
        th: 'Taigo',
        verified: true
      },
      {
        ja: '作物生育制御作業',
        en: 'Handling for plant growth control',
        th: 'Taigo 2',
        verified: false
      },
      {
        ja: '繁殖準備作業',
        en: 'Preparation of plant propagation',
        th: 'Taigo 3',
        verified: false
      }]
    }
  },
  methods: {
    // TODO: Call tranlate API to Google Translate and show the translated back.
    translate (word) {
      console.log(word)
      alert(`Hello ${word}`)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
