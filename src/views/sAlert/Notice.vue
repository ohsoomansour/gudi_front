<template>
  <v-container fluid>
    <v-card class="dashboard-card">
      <v-card-title class="d-flex align-center pe-2">
        <div class="titletext">{{ titleText }}</div>
        <v-spacer></v-spacer>
      </v-card-title>

      <div class="container">
        <div class="filter-button-group">
          <v-btn
            :class="{ 'filter-button': true, active: activeFilter === 'all' }"
            @click="findAll"
            >전체</v-btn
          >
          <v-btn
            :class="{ 'filter-button': true, active: activeFilter === 'admin' }"
            @click="findAdmin"
            >관리자</v-btn
          >
          <v-btn
            :class="{
              'filter-button': true,
              active: activeFilter === 'teacher',
            }"
            @click="findTeacher"
            >강사</v-btn
          >
        </div>

        <div class="search">
          <div class="search-container">
            <v-icon class="search-icon">mdi-magnify</v-icon>
            <input
              type="text"
              class="search-input"
              placeholder="검색어를 입력해주세요."
              v-model="stitle"
            />
          </div>
          <div class="button-group">
            <button class="search-button" @click="searchMethod">검색</button>
          </div>
        </div>
      </div>

      <v-divider></v-divider>

      <v-table class="dashboard-table">
        <thead>
          <tr>
            <th>글번호</th>
            <th>작성자</th>
            <th>제목</th>
            <th>등록일</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>관리자</td>
            <td @click="noticeModify">공지사항입니다.</td>
            <td>2024.01.01</td>
          </tr>
          <tr>
            <td>2</td>
            <td>강사</td>
            <td @click="noticeModify">공지사항2입니다.</td>
            <td>2024.01.01</td>
          </tr>
        </tbody>
      </v-table>
    </v-card>

    <!-- 페이지네이션 추가-->

    <div class="button-group">
      <button class="insert-button" @click="openAddModal">등록</button>
    </div>
    <v-dialog v-model="addModal" max-width="600px">
      <v-card>
        <v-card-text>
          <NoticeModal :action="action" />
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import NoticeModal from "./SNoticeModal.vue";
export default {
  components: {
    NoticeModal,
  },
  data() {
    return {
      titleText: "공지사항",
      addModal: false,
      action: "",
      selectedNotice: null,
      activeFilter: "all",
      stitle: "",
    };
  },
  methods: {
    findAll() {
      this.activeFilter = "all";
    },
    findAdmin() {
      this.activeFilter = "admin";
    },
    findTeacher() {
      this.activeFilter = "teacher";
    },
    searchMethod() {},
    noticeModify(notice) {
      this.selectedNotice = notice;
      this.action = "U";
      this.addModal = true;
    },
    openAddModal() {
      this.action = "";
      this.addModal = true;
    },
    // closeAddModal() {
    //   this.addModal = false;
    // },
  },
};
</script>

<style scoped>
.dashboard-card {
  margin: 20px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  background-color: #fff;
}

.titletext {
  font-size: 24px;
  font-weight: bold;
}

.container {
  display: flex;
  justify-content: space-between;
  height: 50px;
  align-items: center;
}

.filter-button-group {
  display: flex;
  margin: 16px 0;
}

.filter-button {
  background-color: #f4f6f8;
  color: #2c3e50;
  border-radius: 20px;
  padding: 8px 16px;
  margin: 0 4px;
  transition: background-color 0.3s, box-shadow 0.3s;
}

.filter-button.active {
  background-color: #407bff;
  color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.filter-button:hover {
  background-color: #5a9bff;
}

.search {
  display: flex;
  justify-content: flex-end;
}

.search-input {
  flex-grow: 1;
  padding: 8px;
  border: none;
  outline: none;
  font-size: 16px;
}

.button-group {
  text-align: right;
  padding: 16px;
}

.search-button,
.insert-button {
  padding: 10px 17px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.search-button:hover,
.insert-button:hover {
  background-color: #0056b3;
}

.dashboard-table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0;
}

.dashboard-table th,
.dashboard-table td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
  font-size: 16px;
}

.dashboard-table th {
  background-color: #f4f4f4;
  font-weight: bold;
}

.dashboard-table tr:hover {
  background-color: #f1f1f1;
}
</style>
