<template>
  <mu-flat-button label="Download" @click="downloadCSV"/>
</template>

<script>
import json2csv from 'json2csv'

export default {
  props: [
    'wordsFirebase'
  ],
  methods: {
    downloadCSV () {
      let column = [
        'ja',
        'en',
        'th'
      ]
      let columnNames = [
        'Japanese',
        'English',
        'Thai'
      ]
      json2csv({data: this.wordsFirebase, fields: column, fieldNames: columnNames}, (err, result) => {
        if (err) {
          console.log(err)
        }
        let link = document.createElement('a')
        link.href = `data:text/csv;charset=utf-8,${encodeURI(result)}`
        link.target = '_blank'
        link.download = 'cavoc-thai-translated.csv'
        document.body.appendChild(link)
        link.click()
      })
    }
  }
}
</script>

<style>

</style>
