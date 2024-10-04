<template>
    <div class="p-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <NewsCard v-for="article in articles" :key="article.title" :article="article" />
    </div>
  </template>
  
  <script>
  import NewsCard from './NewsCard.vue'
  
  export default {
    components: {
      NewsCard,
    },
    props: {
      articles: Array,
    },
   
  }

  
  </script>
  