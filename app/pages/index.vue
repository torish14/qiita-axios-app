<template>
  <div />
</template>

<script>
export default {
  //! async await で簡潔に非同期処理を実装
  // ? https://qiita.com/soarflat/items/1a9613e023200bbebcb3
  // async は非同期関数を定義する
  async mounted () {
    // eslint-disable-next-line
    console.log(
      JSON.stringify(await // await は結果が返されるまで待機する
      this.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js')
      ), true, ''
    )
  }
}
</script>

<style>

</style>
