<template>

<div class="w-full h-14 grid items-center"></div>

  <div class="w-[100vw] h-[100vh] [&_.leaflet-popup-content-wrapper]:bg-white [&_video]:min-h-36">
    <!-- Times Square -->
    <LMap ref="map" :zoom="zoom" :center="[40.758896, -73.985130]">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />

      <l-marker :lat-lng="[40.781303, -73.974113]">
        <l-popup class="m-3 w-60 max-w-full h-52">
          <h2 class="text-lg m-1 italic">National history museum</h2>
          <h3 class="text-md text-teal-700 m-1">Night at the museum</h3>
          <video controls width="600">
            <source :src="video" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker> 

      <l-marker :lat-lng="[40.766939, -73.973794]">
        <l-popup class="m-3 w-60 max-w-full h-52">
          <h2 class="text-lg m-1 italic">Central Park</h2>
          <h3 class="text-md text-teal-700 m-1">Home Alone 2</h3>
          <video controls width="600">
            <source :src="video2" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker>

      <l-marker :lat-lng="[40.688930, -74.044100]">
        <l-popup class="m-3 w-60 max-w-full h-52">
          <h2 class="text-lg m-1 italic">Liberty statue</h2>
          <h3 class="text-md text-teal-700 m-1">The day after tomorrow</h3>
          <video controls width="600">
            <source :src="video3" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker>

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

import video from '../assets/images/natural-history-museum/nuit-au-musee.mp4';
import video2 from '../assets/images/central-park/home-alone-2-gapstow-bridge.mp4';
import video3 from '../assets/images/liberty-statue/The-Day-After-Tomorrow.mp4';


</script >

<style>
body {
  margin: 0;
}
</style>