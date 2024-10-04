<template>
  <div class="w-full py-4 bg-slate-950">
    <h2 class="text-center">News Hub</h2>
  </div>
  <div class="flex">
    <NavigationDrawer :api_key="api_key" @selectsource="fetchArticles" />
    <div class="flex-1">
      <MainContent :articles="articles" />
    </div>
  </div>
</template>

<script>
import NavigationDrawer from './components/NavigationDrawer.vue'
import MainContent from './components/MainContent.vue'
import { ref } from 'vue'
import axios from 'axios'

export default {
  components: {
    NavigationDrawer,
    MainContent
  },
  setup() {
    const api_key = 'dd96725ea1434eff9f1052dc9ed57ebb' // Replace with your News API key
    const articles = ref([])

    const fetchArticles = async (sourceId) => {
      try {
        const response = await axios.get(`https://newsapi.org/v2/top-headlines?sources=${sourceId}&apiKey=${api_key}`)
        articles.value = response.data.articles
        console.log(response.data.articles);
        
      } catch (error) {
        console.error(error)
      }
    }

    return { api_key, articles, fetchArticles }
  }
}
</script>
