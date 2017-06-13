<template>
  <div id="app">
    <mu-appbar :title="title">
      <add-word-modal slot="right" id="add-word-modal" />
    </mu-appbar>
    <translator-chart :words-firebase="words" :firebase-db="firebaseDatabase"></translator-chart>
  </div>
</template>

<script>
import TranslatorChart from './components/TranslatorChart'
import AddWordModal from './components/AddWordModal'
import Firebase from 'firebase'
import FirebaseConfig from './config/FirebaseConfig'

const firebaseApp = Firebase.initializeApp(FirebaseConfig)
const db = firebaseApp.database()

export default {
  name: 'app',
  components: {
    TranslatorChart,
    AddWordModal
  },
  data () {
    return {
      title: 'CAVOC translator',
      firebaseDatabase: db
    }
  },
  firebase: function () {
    return {
      words: db.ref('words')
    }
  }
}
</script>

<style scoped>
  #add-word-modal {
    height: 100%;
  }
</style>
