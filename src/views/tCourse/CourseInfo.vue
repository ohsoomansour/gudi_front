<template>
  <v-container fluid>
    <v-card class="dashboard-card">
      <div class="titleHeader">
        <v-card-title class="d-flex align-center pe-2">
          <div class="titletext">{{ titleText }}</div>
          <v-spacer></v-spacer>
        </v-card-title>

        <!-- <div class="button-group">
          <button class="goBack-button" @click="goBack">뒤로가기</button>
        </div> -->
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
              <th>현재인원</th>
              <th>수강인원</th>
              <th>수강생조회</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Java 기초</td>
              <td>강사</td>
              <td>101호</td>
              <td>2024.01.02</td>
              <td>2024.05.01</td>
              <td>2</td>
              <td>20</td>
              <td @click="showAttendance" class="showAttendance">명단조회</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>

      <v-card v-if="attendance" class="dashboard-card">
        <div class="titletext">수강생 명단</div>
        <Attendance />
      </v-card>
    </v-card>

    <!-- <div class="button-group">
      <button class="registration-button" @click="lectureRegistration">
        강의신청
      </button>
    </div> -->
  </v-container>
</template>

<script>
import Attendance from "./TStudentApprovalAttendance.vue";
export default {
  components: { Attendance },
  data() {
    return {
      titleText: "강의 수강생 정보",
      selectedLecture: null,
      attendance: false,
    };
  },
  methods: {
    lectureRegistration() {},
    showAttendance(lectureName) {
      this.selectedLecture = lectureName;
      this.attendance = true;
    },
  },
};
</script>

<style scoped>
.showAttendance {
  cursor: pointer;
}
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

.search-button,
.insert-button,
.goBack-button,
.registration-button {
  padding: 10px 17px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.search-button:hover,
.insert-button:hover,
.goBack-button:hover,
.registration-button:hover {
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
