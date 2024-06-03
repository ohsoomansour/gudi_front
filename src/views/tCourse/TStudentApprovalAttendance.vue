<template>
  <v-table class="dashboard-table">
    <thead>
      <tr>
        <th>이름</th>
        <th>연락처</th>
        <th>이메일</th>
        <th>생년월일</th>
        <th>설문</th>
        <th>점수</th>
        <th>승인여부</th>
        <th>승인/취소</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user, index) in users" :key="index">
        <td>{{ user.name }}</td>
        <td>{{ user.phone }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.birthdate }}</td>
        <td>{{ user.survey }}</td>
        <td>{{ user.score }}</td>
        <td>{{ user.approval }}</td>
        <td>
          <button @click="toggleApproval(index)">
            {{ user.approval === "Y" ? "취소" : "승인" }}
          </button>
        </td>
      </tr>
    </tbody>
  </v-table>
</template>

<script>
export default {
  data() {
    return {
      users: [
        {
          name: "홍길동",
          phone: "010-1234-5678",
          email: "gudiedu@naver.com",
          birthdate: "1990-01-01",
          survey: "N",
          score: 0,
          approval: "N",
        },
        {
          name: "김길동",
          phone: "010-1234-5678",
          email: "gudiedu@naver.com",
          birthdate: "1990-01-01",
          survey: "Y",
          score: 0,
          approval: "Y",
        },
      ],
    };
  },
  methods: {
    toggleApproval(index) {
      this.users[index].approval =
        this.users[index].approval === "Y" ? "N" : "Y";
    },
  },
};
</script>

<style scoped>
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
  width: 200px;
}

.dashboard-table th {
  background-color: #f4f4f4;
  font-weight: bold;
}

.dashboard-table tr:hover {
  background-color: #f1f1f1;
}

button {
  padding: 8px 16px;
  border: none;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  border-radius: 4px;
}

button:hover {
  background-color: #0056b3;
}
</style>
