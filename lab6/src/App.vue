<script setup>
    // import VideoPlayer.vue
    import VideoPlayer from './components/VideoPlayer.vue'
    // import VideoDetails.vue
    import VideoDetails from './components/VideoDetails.vue'
</script>

<template>
    <div class="app">
        <VideoPlayer />
        <div class="allDetails">
            <VideoDetails />
            <Chat />
        </div>
    </div>
</template>

<style scoped>
    .app {
        display: flex;
        flex-direction: row;
    }

    .allDetails {
        display: flex;
        flex-direction: column;
    }
</style>