<template>
  <v-table class="dashboard-table">
    <thead>
      <tr>
        <th>수업일자</th>
        <th>강의명</th>
        <th>출결상태</th>
        <th>비고</th>
        <th>첨부파일</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>2024.05.29</td>
        <td>Java 기초</td>
        <td>
          <v-select
            v-model="attendanceStatus"
            :items="attendanceOptions"
            class="fixed-width-select"
          ></v-select>
        </td>
        <td></td>
        <td></td>
      </tr>
      <tr>
        <td>2024.05.30</td>
        <td>Java 기초</td>
        <td>
          <v-select
            v-model="attendanceStatus"
            :items="attendanceOptions"
            class="fixed-width-select"
          ></v-select>
        </td>
        <td></td>
        <td></td>
      </tr>
      <tr>
        <td>2024.06.01</td>
        <td>Java 기초</td>
        <td>
          <v-select
            v-model="attendanceStatus"
            :items="attendanceOptions"
            class="fixed-width-select"
          ></v-select>
        </td>
        <td></td>
        <td></td>
      </tr>
    </tbody>
  </v-table>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      attendanceStatus: null,
      attendanceOptions: ["출석", "지각", "조퇴"],
    };
  },
  methods: {},
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
.fixed-width-select {
  width: 100%;
  min-width: 100px;
  box-sizing: border-box;
  display: flex;
}
</style>
