<template>
  <div class="News">
    <h1>Berita Terkini</h1>
    <ul>
      <li v-for="news in listNews" :key="news.title" @click="goToNewsDetail(news.title)">
        <div><img :src="news.urlToImage" alt="" /></div>
        <div>
          <h5>{{ news.author }}</h5>
          <h3>{{ news.title }}</h3>
          <h5>{{ formatDate(news.publishedAt) }}</h5>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "NewsView",
  methods: {
    fetchNews() {
      this.$store.dispatch("news/fetchNews");
    },
    formatDate(dateString) {
      const options = {
        weekday: "long",
        year: "numeric",
        month: "long",
        day: "numeric",
        hour: "2-digit",
        minute: "2-digit",
      };
      return new Date(dateString).toLocaleDateString("id-ID", options);
    },
    goToNewsDetail(newsTitle) {
      const newsId = this.listNews.find((news) => news.title === newsTitle).title;
      this.$router.push({ name: "newsDetail", params: { id: newsId } });
    },
  },
  computed: {
    listNews() {
      return this.$store.state.news.list;
    },
  },
  mounted() {
    this.fetchNews();
  },
};
</script>

<style>
.News h1 {
  text-align: center;
}
.News ul {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}
.News li {
  background-color: aquamarine;
  display: flex;
  gap: 20px;
  align-items: center;
  width: 45%;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}
li img {
  width: 250px;
  height: 180px;
}
@media screen and (max-width: 1080px) {
  .News li {
    width: 100%;
  }
}
</style>
