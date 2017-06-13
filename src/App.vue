<template>
  <div id="app">
    <mu-appbar :title="title">
      <mu-flat-button label="Add new word" slot="right" @click="addNewWord()"/>
    </mu-appbar>
    <translator-chart :words-firebase="words" :firebase-db="firebaseDatabase"></translator-chart>
    <add-word-modal/>
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
  },
  methods: {
    addNewWord () {
      this.$modal.show('Add new word')
    }
  }
}
</script>

<style>
</style>
