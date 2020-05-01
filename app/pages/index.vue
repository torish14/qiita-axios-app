<template>
  <section class="container">
    <!-- <div> -->
    <header>
      <h1>Nuxt.js のタグが付けられた投稿一覧</h1>
    </header>
    <main>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>
            <a :href="item.url"><span>{{ item.title.slice(0,100) }}</span></a>
            <small>
              <span>by</span>
              <nuxt-link :to="`/users/${ item.user.id }`">
                {{ item.user.id }}
              </nuxt-link>
            </small>
          </h4>
          <div class="body">
            {{ item.body.slice(0, 100) }}・・・
          </div>
        </li>
      </ul>
    </main>
    <!-- </div> -->
  </section>
</template>

<script>
export default {
  //! async await で簡潔に非同期処理を実装
  // ? https://qiita.com/soarflat/items/1a9613e023200bbebcb3
  // async は非同期関数を定義する
  // async mounted () {
  // eslint-disable-next-line
    // console.log(
  // JSON.stringify(await // await は結果が返されるまで待機する
  // this.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js')
  // ), true, ''
  // )
  // }
  //! asyncDataメソッドは、サーバーサイドでデータを取得してレンダリングする場合に用いる
  async asyncData ({ app }) {
    const items = await app.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js')
    return {
      items
    }
  }
}
</script>

<style>
/* 全体 */
.container {
  min-height: 100vh;
  padding: 16px;
}

/* ヘッダー */
h1 {
  margin: 16px;
  padding: 12px;
  border-bottom: solid 1px #e5e5e5;
  background-color: #007acc;
  width: 1160px;
  color: white;
  font-weight: bold;
  font-size: 20px;
}

ul {
  margin-left: 16px;
}

li + li {
  margin: 16px 0;
}

span {
  padding-left: 4px;
  color: rgba(0, 122, 204, 1);
}

/* 投稿文 */
.body {
  font-size: 12px;
}
</style>
