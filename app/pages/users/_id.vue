<template>
  <section class="container">
    <div>
      <h3>{{ user.id }}</h3>
      <img :src="user.profile_image_url" alt="プロフィール画像" width="120">
      <p>{{ user.description || 'No description' }}</p>
      <p>
        <nuxt-link to="/">
          <small><b>トップへ戻る</b></small>
        </nuxt-link>
      </p>
      <h3>{{ user.id }}さんの投稿一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>
            <span>
              {{ item.titile }}
            </span>
          </h4>
          <div>{{ item.body.slice(0, 80) }}・・・</div>
          <p><a :href="item.url" target="_blank">{{ item.url }}</a></p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData ({ route, app }) {
    const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user/${route.params.id}`)
    return { user, items }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  padding: 16px;
}

h3 {
  margin: 16px 0;
  padding: 8px 0;
  border-bottom: solid 1px #e5e5e5;
}

li + li {
  margin: 16px 0;
}

p {
  margin: 6px 0;
}
</style>
