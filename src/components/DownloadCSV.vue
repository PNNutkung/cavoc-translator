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
      json2csv({data: this.wordsFirebase, fields: column}, (err, result) => {
        if (err) {
          console.log(err)
        }
        console.log(result)
      })
    }
  }
}
</script>

<style>

</style>
