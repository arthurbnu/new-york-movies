<template>
  <div class="w-full h-14 flex justify-between items-center bg-gray-900 pr-5">
    <a href="/">
      <h1 class="btn bold btn-ghost text-lg md:text-xl text-teal-600">
        <i class="las la-map-marker"></i>
        New York movies
      </h1>
    </a>
  </div>

  <div class="w-[100vw] h-[75vh]">
    <div class="p-2 text-center ">
      <h2 class="text-teal-500 text-lg inline m-2"> Movies associated with a New York borough</h2>
      <h3 class="italic inline">Wikidata</h3>
    </div>
    <iframe class="w-full h-full" :src="'https://query.wikidata.org/embed.html#' + encodeURIComponent(sparqlRequest)"
      referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>
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

const sparqlRequest =
  `
    #Les films faits dans un quartier de NY
    #defaultView:Map
SELECT ?movie ?movieLabel ?narrative_location ?narrative_locationLabel ?coordinates ?image WHERE {
   ?movie wdt:P840 ?narrative_location ;
          wdt:P31 wd:Q11424 .
          optional {?movie wdt:P18 ?image}
   ?narrative_location wdt:P625 ?coordinates ;
                       wdt:P31 wd:Q408804
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
    `
</script>