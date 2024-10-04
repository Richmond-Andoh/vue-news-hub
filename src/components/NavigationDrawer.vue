<template>
  <div class="relative">
    <!-- Button to toggle the drawer -->
    <button @click="toggleDrawer" class="p-2 bg-blue-500 text-white">
      Toggle Drawer
    </button>

    <!-- Navigation Drawer -->
    <div
      :class="{'-translate-x-full': !drawer, 'translate-x-0': drawer}"
      class="fixed left-0 top-0 w-64 h-full bg-gray-800 text-white transition-transform transform duration-300 z-50"
    >
      <ul class="space-y-4 p-4">
        <li v-for="source in sources" :key="source.id" @click="selectSource(source.id)" class="cursor-pointer hover:bg-gray-700 p-2 rounded-md">
          <div class="flex items-center space-x-4">
            <!-- Avatar -->
            <!-- <img :src="getImgUrl(source.id)" alt="Source Logo" class="w-8 h-8 rounded-full"> -->
            <!-- Source Name -->
            <span>{{ source.name }}</span>
          </div>
        </li>
      </ul>
    </div>

    <!-- Overlay to close drawer -->
    <div
      v-if="drawer"
      @click="toggleDrawer"
      class="fixed inset-0 bg-black bg-opacity-50 z-40"
    ></div>
  </div>
</template>

<script>
import axios from 'axios'
import { ref, onMounted } from 'vue'

export default {
  props: {
    api_key: String,
  },
  setup(props, { emit }) {
    const drawer = ref(false)
    const sources = ref([])

    // Function to get the source image
    const getImgUrl = (pic) => {
      //return require(`../assets/images/${pic}.png`)
    }

    // Function to select a news source
    const selectSource = (source) => {
      emit('selectsource', source)
      toggleDrawer() // Close the drawer when a source is selected
    }

    // Function to toggle the drawer
    const toggleDrawer = () => {
      drawer.value = !drawer.value
    }

    // Fetch the news sources on component mount
    const fetchSources = async () => {
      try {
        const response = await axios.get(`https://newsapi.org/v2/sources?language=en&apiKey=${props.api_key}`)
        sources.value = response.data.sources        
      } catch (error) {
        console.error(error)
      }
    }

    onMounted(fetchSources)

    return {
      drawer,
      sources,
      getImgUrl,
      toggleDrawer,
      selectSource,
    }
  }
}
</script>
