<template>
<div class="w-full h-14 flex justify-between items-center bg-gray-900 pr-5">
  <transition-scale group class="contents" no-opacity>
    <div  v-for="movie in visibleMovies" :key="movie.src" v-show="movie.src == hoveredMovie?.src"
      class="hidden md:block absolute top-4 px-2 left-[45vw] w-56 rounded-lg text-teal-500 animate-pulse z-20 bg-teal-300/20 "
      :class = "{'border-b-2 border-teal-600/35 !animate-none' : movie.src == selectedMovie?.src}"
    >
    <i class="las la-map-marker"></i>
    <span class="">
      {{ hoveredMovie?.title  }} 
    </span>
    </div>
</transition-scale>
  <div class="text-teal-600">
    <a href="">
      <h1 class="btn bold btn-ghost text-lg md:text-xl">
        <i class="las la-map-marker"></i>
        New York movies
      </h1>
    </a>
    <a href="wikidata" class="text-sm hidden md:inline">Wikidata</a>
  </div>
  <div class="w-36 md:w-60 flex items-center gap-2">
    <label for="search" class="text-gray-500 hidden md:block">
      <i class="las la-search inline m-2 "></i>Search</label>
      <input id = "search" type="text" v-model="search" placeholder="movie / place" 
    class=" bg-teal-200 w-full rounded-md h-8 p-1">
  </div>
</div>

  <div class="w-[100vw] h-[66vh]">
    <LMap ref="map" :zoom="zoom" :center="mapCenter">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />

      <VideoMarker v-for="movie in visibleMovies" v-bind="movie" :key="movie.src" @click="selectedMovie = movie"
      @mouseover="hoveredMovie = movie"
      />
    </LMap>
  </div>

  <client-only>
    <div ref = "moviesContainer" class="w-full overflow-scroll p-5 pt-3 md:p-7 bg-slate-900">
      <div class="flex w-[500%] md:w-[250%] gap-5">
        <div v-for="movie in visibleMovies" :key="movie.src">
          <span :class="{'text-teal-200 animate-pulse' : movie.src === selectedMovie?.src}"  
            class="text-teal-600 inline-block max-h-6 overflow-hidden transition-all">{{movie.title}}</span>
          <video controls class="h-32" ref = "videos" :data-src = "movie.src">
            <source :src="movie.src" type="video/mp4"/>
          </video>
        </div>
      </div>
    </div>
  </client-only>
</template>

<script setup>
import ogImage from '@/assets/images/capture.png';
import jsonMovies from '@/assets/movies.json';
const videoGlob = import.meta.glob('@/assets/videos/*/*.mp4', { eager: true })
jsonMovies.forEach(m => m.src = videoGlob[`/assets/videos/${m.path}`].default )

useHead({
      title: 'New York Movies',
      description: 'hang out in NY, find movies',
      link: [
        { rel: 'icon', type: 'image/png', href: '/favicon.png' },
      ],
      meta: [
        {
          hid: 'og:image',
          name: 'og:image',
          property: 'og:image',
          content: ogImage,
        },
      ],
    });
    
const search = ref('')
const videos = ref([])

const mapCenter = ref([40.730824, -73.997330])
const zoom = ref(12)
const selectedMovie = ref()
const hoveredMovie = ref()
const moviesContainer = ref()

const matchSearch = property => property?.toUpperCase().includes(search.value.toUpperCase())

const visibleMovies = computed(() =>
jsonMovies.filter(movie => 
      matchSearch(movie.title) ||
      matchSearch(movie.place) ||
      matchSearch(movie.tags)  
    )
)

watchEffect(() => {
  if (visibleMovies.value.length >=0){
    mapCenter.value = visibleMovies.value[0].coords
  }
})

// watch(hoveredMovie, currentValue => {
//    setTimeout(() => {
//       if (hoveredMovie.value === currentValue) 
//         hoveredMovie.value = null
//     }
//     , 2000)
// })

watchEffect(() => {
  if (selectedMovie.value){
    const vid = videos.value.find(v => v.dataset.src == selectedMovie.value.src)
    moviesContainer.value.scrollLeft = vid.offsetLeft - 10
  }
})

</script >

<style>
body {
  margin: 0;
}
</style>