<template>

<div class="w-full h-14 grid items-center">

</div>

  <div style="height:100vh; width:100vw">
    <LMap ref="map" :zoom="zoom" :center="[40.781303, -73.974113]">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />

      <l-marker :lat-lng="[40.781303, -73.974113]">
        <l-popup class="m-3 w-40">
          <h2 class="text-lg m-1 italic">National history museum</h2>
          <h3 class="text-md text-teal-700 m-1">Night at the museum</h3>
          <video controls width="450">
            <source :src="video" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker>

      <l-marker :lat-lng="[40.766939, -73.973794]">
        <l-popup class="m-3 w-40">
          <h2 class="text-lg m-1 italic">Central Park</h2>
          <h3 class="text-md text-teal-700 m-1">Home Alone 2</h3>
          <video controls width="450">
            <source :src="video2" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker>

    </LMap>
  </div>
</template>

<script setup>
const zoom = ref(12)

import video from '../assets/images/natural-history-museum/nuit-au-musee.mp4';
import video2 from '../assets/images/central-park/home-alone-2-gapstow-bridge.mp4';



//
</script>

<style>
body {
  margin: 0;
}
</style>