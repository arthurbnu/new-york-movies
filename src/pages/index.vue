<template>
<div class="w-full h-14 flex justify-between items-center bg-gray-900 pr-5">
  <h1 class="btn bold btn-ghost text-lg md:text-xl text-teal-600">
      <i class="las la-film "></i>
      <i class="las la-map-marker "></i>
      New York movies
  </h1>
   <input type="text" v-model="search" placeholder="movie / place" 
    class=" bg-teal-200 w-32 md:w-48 rounded-md h-8">
</div>

  <div class="w-[100vw] h-[100vh]">
    <LMap ref="map" :zoom="zoom" :center="mapCenter">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />

      <VideoMarker v-for="(movie, id) in visibleMovies" v-bind="movie" :key="movie.src"/>
    </LMap>
  </div>
</template>

<script setup>
import ogImage from '../assets/images/capture.png';
const search = ref('')

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
    placeName : "Liberty statue",
    title : "The day after tomorrow",
    src : getMovie('liberty-statue/The-Day-After-Tomorrow.mp4'),
    coords : [40.688930, -74.044100]
  },
  {
    placeName : "Central Park",
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
    coords : [40.699215, -73.99903]
  },

]

watchEffect(() => {
  if (visibleMovies.value.length >=0)
    mapCenter.value = [visibleMovies.value[0].coords[0]-.05, visibleMovies.value[0].coords[1]]
})

</script >

<style>
body {
  margin: 0;
}
</style>