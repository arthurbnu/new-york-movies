<template>
    <l-marker :lat-lng="coords" >
        <l-popup class="m-3 w-60 max-w-full h-52">
            <h2 class="text-lg m-1 italic">{{place}}</h2>
            <h3 class="text-md text-teal-700 m-1">{{ title }}</h3>
            <video controls width="600" class="min-h-36">
                <source :src="src" type="video/mp4" />
            </video>
        </l-popup>
    </l-marker> 
</template>

<script setup>

const props = defineProps({
    title : {
        type : String,
        required : true
    },
    src : {
        type : String,
        required : true
    },
    place : {
        type :String,
        required:true
    },
    coords : {
        type : Array,
        required : true
    }
})

</script>