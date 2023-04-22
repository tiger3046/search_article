<template>
    <p>Wellcome to SearchArticle!</p>
    <p>this App is for serching Article from qiita.</p>
    <div>
    <h1>Search Articles</h1>
    <form @submit.prevent="searchArticles">
      <input type="text" v-model="searchQuery" />
      <button type="submit">Search</button>
    </form>
    <ul>
      <li v-for="article in searchResults" :key="article.id">
        <a :href="article.url" target="_blank">{{ article.title }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      searchResults: []
    }
  },
  methods: {
    async searchArticles() {
      const response = await fetch(`https://qiita.com/api/v2/items?query=${this.searchQuery}`, {
        headers: {
          Authorization: `Bearer ${'18ac60e153e39d36c246a942ddb1be6e7a0d121c'}`
        }
      })
      const data = await response.json()
      this.searchResults = data.map(article => ({
        id: article.id,
        title: article.title,
        url: article.url
      }))
    }
  }
}


</script>