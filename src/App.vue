<template>
  <div id="app">
    <mu-appbar :title="title"></mu-appbar>
    <translator-chart :words-ref="words"></translator-chart>
  </div>
</template>

<script>
import TranslatorChart from './components/TranslatorChart'
import Firebase from 'firebase'
import FirebaseConfig from './config/FirebaseConfig'

const firebaseApp = Firebase.initializeApp(FirebaseConfig)
const db = firebaseApp.database()

export default {
  name: 'app',
  components: {
    TranslatorChart
  },
  data () {
    return {
      title: 'CAVOC translator'
    }
  },
  firebase: {
    words: db.ref('words')
  }
}
</script>

<style>
</style>
