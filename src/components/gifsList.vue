<template>
    <div class="list">
        <div v-for="gif in gifs" :key="gif.id">
            <Gif :gif="gif"></Gif>
        </div>
    </div>
</template>
<script>
import Gif from './gifComponent.vue'

export default {
   props: {
    gifs: Array
   },
   components: {
    Gif
   }
}
</script>
<style>
.list {
    margin-top: 20px;
    display: flex;
    flex-wrap: wrap;
}
</style>