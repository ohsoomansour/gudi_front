<template>
  <div class="lecture-detail">
    <h2 class="title">출결</h2>

    <div class="attendanceModal">
      <v-card class="dashboard-card">
        <div class="titletext">강의일정 : 2024.01.02 - 2024.05.01</div>

        <v-table class="dashboard-table">
          <thead>
            <tr>
              <th>총 수강일수</th>
              <th>출석일</th>
              <th>결석일</th>
              <th>출석률(일수)</th>
              <th>총수당지급액</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>100</td>
              <td>90</td>
              <td>1</td>
              <td>90%</td>
              <td>500,000</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>

      <div class="bottom">
        <v-card class="dashboard-card half-width">
          <div class="titletext">특이사항</div>

          <v-table class="dashboard-table">
            <thead>
              <tr>
                <th>결석일자</th>
                <th>출석상태</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>2024.05.22</td>
                <td>결석</td>
              </tr>
            </tbody>
          </v-table>
        </v-card>

        <v-card class="dashboard-card half-width">
          <div class="titletext">수당지급내역</div>

          <v-table class="dashboard-table">
            <thead>
              <tr>
                <th>지급일자</th>
                <th>금액</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>2024.05.24</td>
                <td>250,000</td>
              </tr>
            </tbody>
          </v-table>
        </v-card>
      </div>
    </div>

    <!-- <div class="button-group">
      <template v-if="paction === 'U'">
        <v-btn class="update-button" @click="updateNotice">수정</v-btn>
        <v-btn class="delete-button" @click="deleteNotice">삭제</v-btn>
      </template>
      <template v-else>
        <v-btn class="insert-button" @click="insertNotice">등록</v-btn>
      </template>
    </div> -->
  </div>
</template>

<script>
export default {
  props: {
    action: String,
  },
  data() {
    return {
      paction: this.action,
    };
  },
  methods: {
    updateNotice() {},
    deleteNotice() {},
    insertNotice() {},
  },
};
</script>

<style scoped>
.attendanceModal {
  padding: 16px;
}

.bottom {
  display: flex;
  gap: 16px;
  margin-top: 16px;
}

.half-width {
  flex: 1;
  max-width: 50%;
}

.titletext {
  font-size: 16px;
  font-weight: bold;
}

.lecture-detail {
  padding: 16px;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  margin-top: 16px;
  max-width: 800px;
  margin: auto;
}

.title {
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 16px;
  color: #2c3e50;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}

.form-label {
  font-size: 14px;
  color: #2c3e50;
  margin-bottom: 8px;
}

.form-input,
.form-textarea {
  padding: 10px;
  border: 1px solid #dcdcdc;
  border-radius: 4px;
  font-size: 14px;
  color: #34495e;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #407bff;
  box-shadow: 0 0 4px rgba(64, 123, 255, 0.2);
  outline: none;
}

.form-textarea {
  height: 200px;
  resize: vertical;
}

.button-group {
  display: flex;
  justify-content: flex-end;
  gap: 8px;
}

.update-button,
.delete-button,
.insert-button {
  padding: 10px 16px;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
}

.update-button,
.insert-button {
  background-color: #407bff;
}

.update-button:hover,
.insert-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}

.delete-button {
  background-color: #d32f2f;
}

.delete-button:hover {
  background-color: #e57373;
  box-shadow: 0 4px 8px rgba(211, 47, 47, 0.2);
}
</style>
