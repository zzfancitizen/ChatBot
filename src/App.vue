<template>
    <div id="app">
        <ChatBot />
    </div>
</template>

<script>
import ChatBot from './components/ChatBot.vue';

export default {
    name: 'App',
    components: {
        ChatBot
    }
}
</script>

<style>
body {
    background-color: white;
    font-size: calc(16px + 1vw);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

#app {
    width: 100%;
    max-width: 1200px;
    padding: 20px;
    height: 100%;
    display: flex;
    flex-direction: column;
    background-color: white;
}
</style>
