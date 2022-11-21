<script setup>
    import { onMounted, ref } from 'vue';

    let username = ref('');
    let description = ref('');

    // onMounted
    onMounted (() => {
        const apiUrl = 'https://app.fakejson.com/q/JKUHHJ4q?token=4pxnSrNsVlvtvzD5BQH_xQ';
        fetch(apiUrl)
            .then(res => res.json())
            .then(data => {
                username.value = data.videos[0].username;
                description.value = data.videos[0].description;
            })
    });
</script>

<template>
    <div>
        <h3>{{ username }}</h3>
        <p> {{ description }}</p>
    </div>
</template>

<style scoped>
    div {
        padding: 0 2em;
    }
</style>
