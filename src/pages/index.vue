<template>
<div class="w-full h-14 flex justify-between items-center bg-gray-900 pr-5">
  <h1 class="btn bold btn-ghost text-lg md:text-xl text-teal-600">
      <i class="las la-film "></i>
      <i class="las la-map-marker "></i>
      New York movies
  </h1>
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

      <VideoMarker v-for="movie in visibleMovies" v-bind="movie" :key="movie.src" @click="selectedMovie = movie"/>
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
import ogImage from '../assets/images/capture.png';
const search = ref('')
const videos = ref([])

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
    
const mapCenter = ref([40.730824, -73.997330])
const zoom = ref(12)
const selectedMovie = ref()
const moviesContainer = ref()

const videoGlob = import.meta.glob('../assets/videos/*/*.mp4', { eager: true })
const getMovie = movieName => videoGlob[`../assets/videos/${movieName}`].default

const matchSearch = property => property.toUpperCase().includes(search.value.toUpperCase())

const visibleMovies = computed(() =>
    movies.filter(movie => 
      matchSearch(movie.title) ||
      matchSearch(movie.placeName)   
    )
)

const movies = [
  {
    placeName : "National History Museum",
    title : "Night at the museum",
    src : getMovie('natural-history-museum/nuit-au-musee.mp4'),
    coords : [40.781303, -73.974113]
  },
  {
    placeName : "Gapstow bridge",
    title : "Home Alone 2",
    src : getMovie('central-park/home-alone-2-gapstow-bridge.mp4'),
    coords : [40.766939, -73.973794]
  },
  {
    placeName : "Plaza Hotel",
    title : "Home Alone 2",
    src : getMovie('plaza-hotel/Home Alone - PLAZA HOTEL.mp4'),
    coords : [40.7606, -73.985]
  },
  {
    placeName : "Liberty statue",
    title : "The day after tomorrow",
    src : getMovie('liberty-statue/The-Day-After-Tomorrow.mp4'),
    coords : [40.688930, -74.044100]
  },
  {
    placeName : "Carnegie Hall",
    title : "Home Alone 2",
    src : getMovie('carnegie-hall/Home Alone - CARNEGIE HALL.mp4'),
    coords : [40.7648, -73.9797]
  },
  {
    placeName : "Times Square",
    title : "Vanilla Sky",
    src : getMovie('times-square/Vanilla Sky - TIMES SQUARE.mp4'),
    coords : [40.759296, -73.985573]
  },
  {
    placeName : "Brooklyn Bridge",
    title : "John Wick Chapter 2",
    src : getMovie('brooklyn-bridge/John Wick Chapter 2 - BROOKLYN BRIDGE.mp4'),
    coords : [40.699215, -73.99903]
  },
  {
    placeName : "Manhattan Bridge",
    title : "Independance day",
    src : getMovie('manhattan-bridge/Independence Day - MANHATTAN BRIDGE.mp4'),
    coords : [40.707496, -73.990774]
  },

]

watchEffect(() => {
  if (visibleMovies.value.length >=0)
    mapCenter.value = visibleMovies.value[0].coords
})

watchEffect(() => {
  if (selectedMovie.value){
    const vid = videos.value.find(v => v.dataset.src == selectedMovie.value.src)
    moviesContainer.value.scrollLeft = vid.offsetLeft
  }
})

</script >

<style>
body {
  margin: 0;
}
</style>