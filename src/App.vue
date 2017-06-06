<template>
  <div id="app">
    <mu-appbar :title="title"></mu-appbar>
    <translator-chart></translator-chart>
  </div>
</template>

<script>
import TranslatorChart from './components/TranslatorChart'

export default {
  name: 'app',
  components: {
    TranslatorChart
  },
  data () {
    return {
      title: 'CAVOC translator'
    }
  }
}
</script>

<style>
</style>
