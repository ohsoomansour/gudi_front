<template>

  <div id="app">
    <div class="chat-list-container">
      <chat-list :chats="chats" @select-chat="selectChat"></chat-list>
    </div>
    <div class="chat-room-container">
      <chat-room v-if="selectedChat" :chat-room="selectedChat"></chat-room>
    </div>
  </div>
    

</template>

<script>

import ChatList from './ChatList.vue';
import ChatRoom from './ChatRoom.vue';


export default {
  data: function () {
    return {
      chats: [
        { id: 1, name: 'Chat Room 1', participants: 3 },
        { id: 2, name: 'Chat Room 2', participants: 5 }
      ], // 채팅방 목록 데이터
      selectedChat: null // 선택된 채팅방

    };
  },
  mounted() {
    this.searchlist();
  },
  methods: {
    selectChat(chat) {
      this.selectedChat = chat;
    },
    searchlist: function () {
      let vm = this;



      this.axios
        .post("")
        .then((response) => {
          console.log(JSON.stringify(response));

          vm.list = response.data.list;
        })
        .catch(function (error) {
          alert("에러! API 요청에 오류가 있습니다. " + error);
        });
    },
  },

  components: {
    ChatList,
    ChatRoom
  },
};
</script>

<style>

</style>
