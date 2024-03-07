<template>

<div class="w-full h-14 grid items-center"></div>

  <div class="w-[100vw] h-[100vh] [&_.leaflet-popup-content-wrapper]:bg-white [&_video]:min-h-36">

    <LMap ref="map" :zoom="zoom" :center="[40.758896, -73.985130]">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />

      <VideoMarker v-for="movie in movies" v-bind="movie" :key="movie.title"/>

    </LMap>
  </div>
</template>

<script setup>
import ogImage from '../assets/images/capture.png';

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
    
const zoom = ref(12)

const videoGlob = import.meta.glob('../assets/videos/*/*.mp4', { eager: true })
const getMovie = movieName => videoGlob[`../assets/videos/${movieName}`].default

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


]

</script >

<style>
body {
  margin: 0;
}
</style>