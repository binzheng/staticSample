<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>
</template>

<script>
export default {
  data() {
    return {
      headers: [],
      desserts: [],
    }
  },
  created() {
    const config = {
      headers: { 'Content-Type': 'application/json', 'Cache-Control': 'no-cache' },
    }
    const self = this
    this.$axios
      .get('https://staticsamplefun.azurewebsites.net/api/StaticWebApi', config)
      .then((response) => {
        console.log('response : ' + JSON.stringify(response))
        self.headers = response.data.headers
        self.desserts = response.data.desserts
      })
      .catch((error) => {
        console.log('お知らせマスタ一覧を取得エラー' + error)
      })
      .finally(() => {})
  },
}
</script>

<style></style>
