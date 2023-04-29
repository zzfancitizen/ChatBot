<template>
    <div class="chatbot-container">
        <h2>ChatBot</h2>
        <div class="chat-container">
            <div v-for="(message, index) in messages" :key="index" class="message">
                <span :class="message.sender">{{ message.text }}</span>
            </div>
        </div>
        <div class="input-container">
            <input v-model="userInput" @keyup.enter="sendMessage" type="text" placeholder="Type your message">
            <button @click="sendMessage" class="send-button">
                <i class="fas fa-paper-plane"></i>
            </button>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            userInput: '', // User input
            messages: [ // Messages array
                {sender: 'bot', text: 'Bot: Hello! I am ChatBot.'}
            ]
        }
    },
    methods: {
        async sendMessage() { // Send message
            if (this.userInput.trim()) {
                this.messages.push({sender: 'user', text: `User: ${this.userInput}`});
                const response = await this.getBotResponse(this.userInput);
                this.messages.push({sender: 'bot', text: `Bot: ${response.data}`});
            }
        },
        async getBotResponse(userInput) {
            try {
                const response = await axios.post('http://localhost:5000/ask', {
                    question: userInput
                });
                return response.data;
            } catch (error) {
                console.error('Error getting response from external service:', error);
                return 'An error occurred while fetching the response.';
            }
        }
    }
}
</script>

<style scoped>
.chatbot-container {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 20px;
}

.chat-container {
    flex-grow: 1;
    overflow-y: auto;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 5px;
    margin-bottom: 20px;
}

.message {
    padding: 5px;
}

.message .user {
    color: blue;
}

.message .bot {
    color: red;
}

.input-container {
    display: flex;
    align-items: center;
}

input {
    flex-grow: 1;
    border-radius: 5px;
    border: 1px solid #ccc;
    padding: 5px;
}

.send-button {
    background-color: blue;
    border: none;
    color: white;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 5px;
}

.send-button:hover {
    background-color: #add8e6;
}

.fas {
    font-family: 'Font Awesome 5 Free';
    font-weight: 900;
}

h2 {
    color: black;
    text-align: center;
}
</style>

