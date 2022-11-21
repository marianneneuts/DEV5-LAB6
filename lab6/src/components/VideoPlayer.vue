<script setup>
    import { onMounted, reactive, ref } from 'vue';
    import 'animate.css';

    let videos = reactive({data: []});
    let videoSrc = ref('');
    let counter = ref(0);
    let animation = ref('');

    // onMounted
    onMounted (() => {
        const apiUrl = 'https://app.fakejson.com/q/JKUHHJ4q?token=4pxnSrNsVlvtvzD5BQH_xQ';
        fetch(apiUrl)
            .then(res => res.json())
            .then(data => {
                videos.data = data.videos;
                videoSrc.value = data.videos[0].video;
            })
    });

    const nextVideo = () => {
        animation.value = 'animate__fadeOut';
        counter.value++;
        setTimeout(() => {
            videoSrc.value = videos.data[counter.value].video;
            animation.value = 'animate__fadeIn';
        }, 500);
    }
</script>

<template>
    <div class="blur">
        <div class="controls">
            <a @click.prevent="nextVideo" href="#">></a>
        </div>
        <video :src="videoSrc" :class="animation" class="animate__animated" controls autoplay muted></video>
    </div>
</template>

<style scoped>
    video {
        max-width: 100%;
        max-height: 90vh;
    }

    .blur {
        background-image: url('/Blur.jpg');
        background-size: cover;
        position: relative;
        padding: 1em 5em;
    }

    .controls {
        position: absolute;
        top: 11.1%;
        left: 50%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        width: 100%;
    }

    a {
        color: white;
        font-size: 2em;
        text-decoration: none;
    }
</style>
