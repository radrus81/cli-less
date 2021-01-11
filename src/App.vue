<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span>Открыто:{{ openRate }} | Прочитано:{{ readRate }}</span>
      <app-news
        v-for="item in news"
        :key="item.id"
        :title="item.title"
        :id="item.id"
        :is-open="item.isOpen"
        @open-news="openNews"
        @readed-news="readedNews"
        :was-read="item.wasRead"
      >
      </app-news>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import AppNews from './components/AppNews.vue'

export default {
  name: 'App',
  data() {
    return {
      openRate: 0,
      readRate: 0,
      now: new Date().toLocaleDateString(),
      news: [
        { id: 1, title: 'Новость 1', isOpen: false, wasRead: false },
        { id: 2, title: 'Новость 2', isOpen: false, wasRead: false },
        { id: 3, title: 'Новость 3', isOpen: false, wasRead: false },
      ],
    }
  },
  components: {
    Header,
    AppNews,
  },
  methods: {
    openNews() {
      this.openRate++
    },
    readedNews(id) {
      const idx = this.news.findIndex((item) => item.id === id)
      this.news[idx].wasRead = true
      this.readRate++
    },
  },
  provide() {
    return {
      titleAll: 'provide->inject',
      newsAll: this.news,
    }
  },
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h2 {
  color: darkblue;
}
</style>
