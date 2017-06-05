<template>
  <div class="hello">
    <mu-table id="translating-table" :showCheckbox="showCheckbox">
      <mu-thead>
        <mu-th>
          Japanese
        </mu-th>
        <mu-th>
          English
        </mu-th>
        <mu-th>
          Thai
        </mu-th>
      </mu-thead>
      <mu-tbody>
        <mu-tr v-for="word in words" :key="word.id">
          <mu-td>
            {{word.jp}}
          </mu-td>
          <mu-td>
            {{word.en}}
          </mu-td>
          <mu-td>
            {{word.th}}
          </mu-td>
        </mu-tr>
      </mu-tbody>
    </mu-table>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      showCheckbox: false,
      words: [{
        jp: '農作業',
        en: 'Agriculture activity',
        th: 'Taigo'
      },
      {
        jp: '作物生育制御作業',
        en: 'Handling for plant growth control',
        th: 'Taigo 2'
      },
      {
        jp: '繁殖準備作業',
        en: 'Preparation of plant propagation',
        th: 'Taigo 3'
      }]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
