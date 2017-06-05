<template>
  <div id="app">
    <mu-appbar title="Cavoc translator"></mu-appbar>
    <hello></hello>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  }
}
</script>

<style>
</style>
