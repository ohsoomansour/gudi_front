<template>
  <v-container fluid>
    <v-card class="dashboard-card">
      <div class="titleHeader">
        <v-card-title class="d-flex align-center pe-2">
          <div class="titletext">{{ titleText }}</div>
          <v-spacer></v-spacer>
        </v-card-title>

        <div class="button-group">
          <button class="goBack-button" @click="goBack">뒤로가기</button>
        </div>
      </div>

      <v-divider></v-divider>

      <v-card class="dashboard-card">
        <div class="titletext">강의 정보</div>
        <v-table class="dashboard-table">
          <thead>
            <tr>
              <th>강의명</th>
              <th>강사명</th>
              <th>강의실</th>
              <th>시작일</th>
              <th>종료일</th>
              <th>수강인원</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Java 기초</td>
              <td>강사</td>
              <td>101호</td>
              <td>2024.01.02</td>
              <td>2024.05.01</td>
              <td>20</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>

      <v-card class="dashboard-card">
        <div class="titletext">강의 소개</div>

        <v-textarea
          class="textarea"
          label="강의소개"
          model-value="안녕하세요 Java강의에 오신걸 환영합니다."
          readonly
          row-height="30"
          rows="5"
          variant="outlined"
          auto-grow
          shaped
        ></v-textarea>
      </v-card>

      <v-card class="dashboard-card">
        <div class="titletext">주차별 계획</div>
        <v-table class="dashboard-table">
          <thead>
            <tr>
              <th>주차</th>
              <th>학습목표</th>
              <th>학습내용</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1주차</td>
              <td>java</td>
              <td>배열</td>
            </tr>
            <tr>
              <td>2주차</td>
              <td>java</td>
              <td>문법</td>
            </tr>
            <tr>
              <td>3주차</td>
              <td>java</td>
              <td>문법</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>

      <v-card class="dashboard-card">
        <div class="titletext">진도 현황</div>
        <v-table class="dashboard-table">
          <thead>
            <tr>
              <th>총 수업 일</th>
              <th>현 수업 일</th>
              <th>진행률</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>100일</td>
              <td>2일</td>
              <td>2%</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>
      <div class="button-group">
        <v-btn class="update-button" @click="updateLecture">수정</v-btn>
        <v-btn class="delete-button" @click="deleteLecture">삭제</v-btn>
      </div>

      <v-dialog v-model="updateLectureModal" max-width="700px">
        <v-card>
          <v-card-text>
            <LectureManagementModal :action="action" />
          </v-card-text>
        </v-card>
      </v-dialog>
    </v-card>
  </v-container>
</template>

<script>
import LectureManagementModal from "./TCourseModal.vue";
export default {
  components: { LectureManagementModal },
  data() {
    return {
      titleText: "강의상세",
      action: "",
      updateLectureModal: false,
    };
  },
  methods: {
    updateLecture() {
      this.action = "U";
      this.updateLectureModal = true;
    },
  },
};
</script>

<style scoped>
.textarea {
  margin-top: 20px;
}

.titleHeader {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

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

.update-button,
.delete-button,
.insert-button,
.goBack-button {
  /* padding: 10px 16px; */
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
}

.update-button,
.insert-button,
.goBack-button {
  background-color: #407bff;
}

.update-button:hover,
.insert-button:hover,
.goBack-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}

.delete-button {
  background-color: #d32f2f;
  margin: 0;
}

.delete-button:hover {
  background-color: #e57373;
  box-shadow: 0 4px 8px rgba(211, 47, 47, 0.2);
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
