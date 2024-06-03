<template>
  <v-card class="registration-card">
    <v-card-title class="d-flex align-center">
      <div class="titletext">회원등록</div>
      <v-spacer></v-spacer>
    </v-card-title>

    <v-card-text>
      <v-form>
        <div class="form-group">
          <v-select
            :items="memberTypes"
            label="회원유형"
            v-model="formData.memberType"
            outlined
            dense
          ></v-select>
        </div>
        <div class="form-group">
          <v-text-field
            label="이름"
            v-model="formData.name"
            outlined
            dense
          ></v-text-field>
        </div>
        <div class="form-group">
          <v-text-field
            label="아이디"
            v-model="formData.username"
            outlined
            dense
          ></v-text-field>
        </div>
        <div class="form-group">
          <v-text-field
            label="비밀번호"
            type="password"
            v-model="formData.password"
            outlined
            dense
          ></v-text-field>
        </div>
        <div class="form-group">
          <v-text-field
            label="비밀번호 확인"
            type="password"
            v-model="formData.confirmPassword"
            outlined
            dense
          ></v-text-field>
        </div>

        <div class="form-group">
          <v-select
            :items="genders"
            label="성별"
            v-model="formData.gender"
            outlined
            dense
          ></v-select>
        </div>
        <div class="form-group">
          <div class="form-label">생년월일</div>
          <div class="birthdate-select">
            <v-select
              v-model="formData.selectedYear"
              :items="years"
              label="년"
              dense
            ></v-select>
            <v-select
              v-model="formData.selectedMonth"
              :items="months"
              label="월"
              dense
            ></v-select>
            <v-select
              v-model="formData.selectedDay"
              :items="days"
              label="일"
              dense
            ></v-select>
          </div>
        </div>
        <div class="form-group">
          <template v-if="paction === 'U'">
            <div>
              <v-btn class="update-button" @click="updateMember">수정</v-btn>
              <v-btn class="delete-button" @click="deleteMember">삭제</v-btn>
            </div>
          </template>

          <template v-else>
            <v-btn class="register-button" @click="registerMember">등록</v-btn>
          </template>
        </div>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: {
    action: String,
  },
  data() {
    return {
      formData: {
        memberType: "",
        name: "",
        username: "",
        password: "",
        confirmPassword: "",

        gender: "",
        selectedYear: null,
        selectedMonth: null,
        selectedDay: null,
      },
      memberTypes: ["강사", "학생"],
      genders: ["남", "여"],
      years: [],
      months: [],
      days: [],
      paction: this.action,
    };
  },
  mounted() {
    this.initializeDates();
  },
  methods: {
    initializeDates() {
      // 년도 선택을 위한 배열 생성 (예: 1950부터 현재 년도까지)
      const currentYear = new Date().getFullYear();
      for (let year = 1950; year <= currentYear; year++) {
        this.years.push(year);
      }

      // 월 선택을 위한 배열 생성 (1부터 12까지)
      for (let month = 1; month <= 12; month++) {
        this.months.push(month);
      }

      // 일 선택을 위한 배열 생성 (1부터 31까지)
      for (let day = 1; day <= 31; day++) {
        this.days.push(day);
      }
    },
    registerMember() {},
    delMember() {},
  },
};
</script>

<style scoped>
.registration-card {
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

.form-group {
  margin-bottom: 16px;
  text-align: right;
}

.form-label {
  text-align: left;
}

.postal-code-group {
  display: flex;
  align-items: center;
}

.register-button,
.update-button {
  /* padding: 10px 17px; */
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.register-button:hover,
.update-button:hover {
  background-color: #0056b3;
}

.delete-button {
  /* padding: 10px 17px; */
  background-color: #d32f2f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin: 0;
}

.delete-button:hover {
  background-color: #a33030;
}
</style>
