<template>
    <div class="gif-container">
        <h1>I Wuv You</h1>
        <img :src="gifSrc" alt="Valentine's Gif">
    </div>

</template>

<script>
export default {
    name: "GifDisplay",
    props: {
        gifSrc: String,
    },
}

</script>

<style scoped>
.gif-container {
    text-align: center;
    display: block;
}

img {
    max-width: 100%;
    width: 500px;
    height: auto;
}

h1 {
    color: white;
    font-family: 'Times New Roman', Times, serif;
    font-size: 5em;
}

</style>