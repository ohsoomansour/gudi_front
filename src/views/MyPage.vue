<template>
  <v-container fluid>
    <v-card class="dashboard-card">
      <v-card-title class="titleHeader">
        <div class="titletext">마이페이지</div>
      </v-card-title>

      <v-divider></v-divider>

      <v-form>
        <v-card class="dashboard-card">
          <v-card-title class="subtitletext">회원정보 수정</v-card-title>

          <v-container class="container">
            <div class="left">
              <v-select
                :items="memberTypes"
                v-model="user.memberType"
                label="회원유형"
                required
              ></v-select>

              <v-text-field
                v-model="user.name"
                label="이름"
                required
              ></v-text-field>

              <v-text-field
                v-model="user.username"
                label="아이디"
                required
              ></v-text-field>

              <v-text-field
                v-model="user.email"
                label="이메일"
                required
              ></v-text-field>

              <v-text-field
                v-model="user.phone"
                label="전화번호"
                required
              ></v-text-field>
            </div>

            <div class="right">
              <v-select
                :items="genders"
                v-model="user.gender"
                label="성별"
                required
              ></v-select>

              <div class="form-label">
                생년월일
                <div class="birthdate-select">
                  <v-select
                    v-model="user.selectedYear"
                    :items="years"
                    label="년"
                    dense
                  ></v-select>
                  <v-select
                    v-model="user.selectedMonth"
                    :items="months"
                    label="월"
                    dense
                  ></v-select>
                  <v-select
                    v-model="user.selectedDay"
                    :items="days"
                    label="일"
                    dense
                  ></v-select>
                </div>
              </div>
            </div>
          </v-container>
        </v-card>

        <v-card class="dashboard-card">
          <v-card-title class="subtitletext">비밀번호 변경</v-card-title>
          <v-container class="container">
            <div class="left">
              <v-text-field
                v-model="password.current"
                :type="'password'"
                label="현재 비밀번호"
                required
              ></v-text-field>

              <v-text-field
                v-model="password.new"
                :type="'password'"
                label="새 비밀번호"
                required
              ></v-text-field>

              <v-text-field
                v-model="password.confirm"
                :type="'password'"
                label="새 비밀번호 확인"
                required
              ></v-text-field>
            </div>
          </v-container>
        </v-card>

        <div class="form-group">
          <v-btn class="update-button" @click="updateMember">수정</v-btn>
        </div>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      user: {
        memberType: "",
        name: "",
        username: "",
        password: "",
        confirmPassword: "",
        postalCode: "",
        address: "",
        detailAddress: "",
        gender: "",
        selectedYear: null,
        selectedMonth: null,
        selectedDay: null,
      },
      password: {
        current: "",
        new: "",
        confirm: "",
      },
      memberTypes: ["관리자", "강사", "학생"],
      genders: ["남", "여"],
      years: [],
      months: [],
      days: [],
    };
  },
  mounted() {
    this.initializeDates();
  },
  methods: {
    updateMember() {},
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
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
}

.left,
.right {
  width: 50%;
  padding: 20px;
}

.titleHeader {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.titletext {
  font-size: 24px;
  font-weight: bold;
}

.subtitletext {
  font-size: 20px;
  font-weight: bold;
}

.dashboard-card {
  margin: 20px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  background-color: #fff;
}

.form-group {
  margin-bottom: 16px;
  text-align: right;
}

.update-button {
  /* padding: 10px 17px; */
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.update-button:hover {
  background-color: #0056b3;
}
</style>
