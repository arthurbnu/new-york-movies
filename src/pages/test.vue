<template>
  <div style="height:100vh; width:100vw">
    <LMap ref="map" :zoom="zoom" :center="[47.21322, -1.559482]">
      <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&amp;copy; <a href=&quot;https://www.openstreetmap.org/&quot;>OpenStreetMap</a> contributors"
        layer-type="base" name="OpenStreetMap" />


      <l-marker :lat-lng="[47.21322, -1.559482]">
        <l-popup class="m-3 w-40">
          <video controls width="450">
            <source :src="video" type="video/mp4" />
          </video>
        </l-popup>
      </l-marker>


    </LMap>
  </div>
</template>

<script setup>
const zoom = ref(6)

import video from '../assets/images/Shaun-the-Sheep-The-Movie-Official-Trailer.mp4';


//
</script>

<style>
body {
  margin: 0;
}
</style>