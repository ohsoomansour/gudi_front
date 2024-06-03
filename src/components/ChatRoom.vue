<template>
  <div class="chat-room">
    <div class="chat-room-header">
      <div class="chat-room-name">{{ chatRoom.name }}</div>
      <div class="chat-room-participants">{{ chatRoom.participants }}명 참여</div>
    </div>
    <div class="chat-messages">
      <div
        v-for="message in messages"
        :key="message.id"
        :class="{'message-right': message.sender === 'me', 'message-left': message.sender !== 'me'}"
        class="chat-message"
      >
        <div class="message-sender">{{ message.sender }}</div>
        <div class="message-content">{{ message.content }}</div>
        <div v-if="message.sender === 'me' && message.unreadCount > 0" class="message-unread">
          {{ message.unreadCount }}
        </div>
      </div>


    </div>
    <div class="chat-input">
      <input type="text" v-model="newMessage" @keyup.enter="sendMessage">
      <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
// import { Client } from '@stomp/stompjs';
// import SockJS from 'sockjs-client';

export default {
  props: ['chatRoom'],
  data() {
    return {
      client: null,
      connected: false,
      newMessage: '',
      messages: []
    };
  },
  methods: {
  
   }
};
</script>

<style scoped>
</style>
