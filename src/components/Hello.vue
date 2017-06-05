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
        <mu-tr>
          <mu-td>
            nihon go
          </mu-td>
          <mu-td>
            ei go
          </mu-td>
          <mu-td>
            tai go
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
      showCheckbox: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
