<template>
  <div id="comnCodMgr">
    <p class="Location">
      <a href="/dashboard/home" class="btn_set home"></a>
      <span class="btn_nav bold">기준정보</span>
      <span class="btn_nav bold">테스트 / </span>
      <router-link to="/dashboard/sampletest/samplepage3">새로고침</router-link>
    </p>

    <p class="conTitle">
      <span>테스트2번</span>
      <span>
        <table
          style="border: 1px #50bcdf"
          width="100%"
          cellpadding="5"
          cellspacing="0"
          border="1"
          align="left"
        >
          <tr style="border: 0px; border-color: blue">
            <td
              width="50"
              height="25"
              style="font-size: 100%; text-align: left"
            >
            </td>
          </tr>
        </table>
      </span>
    </p>

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
    
    




  </div>
</template>

<script>

export default {
  data: function () {
    return {
      list: [],
      chatRoom: {
        name: '친구들',
        participants: 3
      },
      messages: [
        { id: 1, sender: 'Alice', content: '안녕하세요', unreadCount: 0 },
        { id: 2, sender: 'me', content: '안녕하세요, 잘 지내세요?', unreadCount: 1 },
        { id: 3, sender: 'Bob', content: '네, 잘 지내요!', unreadCount: 0 },
        { id: 4, sender: 'me', content: '좋아요!', unreadCount: 2 }
      ],
      newMessage: ''

    
  
    };
  },
  mounted() {
    this.searchlist();
  },
  methods: {
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
    sendMessage() {
      if (this.newMessage.trim() !== '') {
        this.messages.push({
          id: this.messages.length + 1,
          sender: 'me',
          content: this.newMessage,
          unreadCount: 0
        });
        this.newMessage = '';
      }
    }

  },

  components: { },
};
</script>

<style></style>
