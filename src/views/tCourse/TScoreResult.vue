<template>
  <v-table class="dashboard-table">
    <thead>
      <tr>
        <th>학생이름</th>
        <th>점수</th>
        <th>응시 날짜</th>
        <th>합격 여부</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="result in filteredResults" :key="result.studentName">
        <td>{{ result.studentName }}</td>
        <td>{{ result.score }}</td>
        <td>{{ result.date }}</td>
        <td>{{ result.pass }}</td>
      </tr>
    </tbody>
  </v-table>
</template>

<script>
export default {
  props: {
    lectureName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      // 시험 결과 데이터를 여기에 추가
      results: [
        {
          studentName: "홍길동",
          score: 100,
          date: "2024.05.30",
          pass: "Y",
          lecture: "Java 기초",
        },
        {
          studentName: "김길동",
          score: 55,
          date: "2024.05.30",
          pass: "N",
          lecture: "Java 기초",
        },
        {
          studentName: "박길동",
          score: 75,
          date: "2024.05.30",
          pass: "Y",
          lecture: "Vue",
        },
        {
          studentName: "이길동",
          score: 40,
          date: "2024.05.30",
          pass: "N",
          lecture: "Vue",
        },
      ],
    };
  },
  computed: {
    filteredResults() {
      return this.results.filter(
        (result) => result.lecture === this.lectureName
      );
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
