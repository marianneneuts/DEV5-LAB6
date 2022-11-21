<script setup>
    import { onMounted, reactive, ref } from 'vue';

    let chats = reactive({chats: []});
    let text = ref('');

    // onMounted
    onMounted (() => {
        const apiUrl = 'https://lab5-p379.onrender.com/api/v1/messages/';
        fetch(apiUrl)
            .then(res => res.json())
            .then(data => {
                // console.log(chats);
                chats.chats = data;
            })
    });
</script>

<template>
    <div>
        <div class="chat">
            <ul>
                <li v-for="chat in chats.chats" :key="chats.id">
                    <p><strong><mark>{{ chat.user }}</mark></strong>: {{ chat.text }}</p>
                </li>
            </ul>
        </div>
     </div>
</template>

<style scoped>
    ul {
        list-style: none;
    }
</style>
