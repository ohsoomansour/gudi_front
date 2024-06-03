<template>
  <div>
    <TableViewWithModal
      :headerTitle="title"
      :columns="tableColumns"
      :data="noticeList"
      :options="filterOptions"
      :modalComponentMap="modalComponentMap"
      :isModal="true"
      :searchMethod="searchList"
      @search="searchList"
    />
  </div>
  <div class="button-group">
    <button class="update-button" @click="openAddModal">등록</button>
  </div>
  <v-dialog v-model="addModal" max-width="600px">
    <v-card>
      <v-card-text>
        <ANoticeDetail />
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import TableViewWithModal from "../../components/common/TableViewWithModal.vue";
import ANoticeDetail from "./NoticeDetail.vue";

export default {
  components: {
    TableViewWithModal,
    ANoticeDetail,
  },
  data() {
    return {
      stitle: "",
      ssdate: "",
      sedate: "",
      totalCnt: 1,
      pageSize: 10,
      currentPage: 1,
      noticeList: [],
      title: "공지사항",
      currentFilter: "all",
      filterOptions: [
        { label: "전체", value: "all" },
        { label: "관리자", value: "admin" },
        { label: "강사", value: "teacher" },
      ],
      filterValue: "all",
      tableColumns: ["No", "제목", "등록일", "작성자"],
      //   modalComponentMap: {
      //     ntc_title: ANoticeDetail,
      //     // 필요한 경우 다른 모달 컴포넌트들을 여기에 추가합니다.
      //   },
      addModal: false,
    };
  },
  mounted() {
    this.searchList();
  },
  methods: {
    openAddModal() {
      this.addModal = true;
    },
    closeAddModal() {
      this.addModal = false;
    },
    searchList(stitle, filterValue) {
      let vm = this;

      if (filterValue !== undefined) {
        vm.filterValue = filterValue;
      }

      if (stitle !== undefined) {
        vm.stitle = stitle;
      }

      let params = new URLSearchParams();
      params.append("stitle", this.stitle);
      params.append("ssdate", this.ssdate);
      params.append("sedate", this.sedate);
      params.append("currentPage", this.currentPage);
      params.append("pageSize", this.pageSize);
      params.append("filterValue", this.filterValue);

      this.axios
        .post("/sampletest/listNotice.do", params)
        .then((response) => {
          //console.log(JSON.stringify(response));
          //console.log(response.data);
          var resultTest = response.data.listData;
          //console.log(resultTest);
          vm.noticeList = resultTest.map((result) => {
            return {
              ntc_no: result.ntc_no,
              ntc_title: result.ntc_title,
              ntc_regdate: result.ntc_regdate,
              writer: result.writer,
            };
          });
          console.log(this.noticeList);

          //reduce 함수는 배열의 각 요소를 순회하면서 하나의 값을 누적하는 데 사용
          //여기서는 초기값으로 빈 객체 {}를 사용, acc는 누적된 객체 나타냄
          //ntc_title 값을 키로 하고, 그에 대응하는 값으로 ANoticeDetail 컴포넌트를 설정
          //return acc;는 갱신된 누적 객체를 반환
          vm.modalComponentMap = resultTest.reduce((acc, result) => {
            acc[result.ntc_title] = ANoticeDetail;
            return acc;
          }, {});

          vm.totalCnt = response.data.totalCnt;
        })
        .catch(function (error) {
          alert("에러! API 요청에 오류가 있습니다. " + error);
        });
    },
  },
};
</script>

<style>
.button-group {
  display: flex;
  justify-content: flex-end;
}

.update-button {
  padding: 10px 16px;
  background-color: #407bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-right: 15px;
}

.update-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}
</style>

<style>
.button-group {
  display: flex;
  justify-content: flex-end;
}

.update-button {
  padding: 10px 16px;
  background-color: #407bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-right: 15px;
}

.update-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}
</style>
