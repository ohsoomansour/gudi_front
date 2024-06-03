<template>
  <div id="comnCodMgr">
    <p class="Location">
      <a href="/dashboard/home" class="btn_set home"></a>
      <span class="btn_nav bold">기준정보</span>
      <span class="btn_nav bold">테스트 / </span>
      <router-link to="/dashboard/sampletest/samplepage3">새로고침</router-link>
    </p>

    <p class="conTitle">
      <span>실시간테스트</span>
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
    
<button @click="openChatWindow">채팅테스트</button>



  </div>
</template>

<script>

export default {
  data: function () {
    return {
      list: [],
      

    
  
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
    openChatWindow() {
      
      window.open('#/test', '_blank', 'width=650,height=600');
  }

  },

  components: { },
};
</script>

<style></style>
