<template>
    <div>
        <div :style="`background-image: url(${gif.images.fixed_width.url}); height: 200px; width: 200px;`" class="gif">.</div>
    </div>
</template>
<script>
export default {
    props: {
        gif: Object
    }
}
</script>
<style>
.gif {
    background-repeat: no-repeat;
}
</style>