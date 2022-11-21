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

    const addChat = () => {
        let newChat = {
            user: 'Marianne',
            text: text.value
        }
        
        const apiUrl = 'https://lab5-p379.onrender.com/api/v1/messages/';
        fetch(apiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(newChat)
        })
        .then(res => res.json())
        .then(data => {
            chats.chats.push({
                user: data.data.user,
                text: data.data.text
            });
        })

        // error handling
        .catch((error) => {
            console.error('Error:', error);
        });
    }
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
        <div class="input">
            <input type="text" v-model="text" />
            <button @click="addChat">Add comment</button>
        </div>
    </div>
</template>

<style scoped>
    ul {
        list-style: none;
    }

    .input {
        padding-left: 2.5em;
    }
</style>
