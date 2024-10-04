<template>
    <div class="bg-white shadow-lg rounded-lg overflow-hidden">
      <img :src="article.urlToImage" class="w-full h-48 object-cover" />
      <div class="p-4">
        <h3 class="text-lg font-bold">{{ article.title }}</h3>
        <p class="text-gray-600">{{ article.description }}</p>
        <p class="flex justify-between align-middle">
            <a :href="article.url" target="_blank" class="text-blue-500 mt-2 inline-block">Read More</a>
            <span class="text-blue-500 mt-2 inline-block">{{ article.publishedAt }}</span>
        </p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      article: Object,
    },
    
  }
  </script>
  