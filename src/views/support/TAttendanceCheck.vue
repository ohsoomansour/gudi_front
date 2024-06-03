<template>
  <div>
    <v-table class="dashboard-table">
      <thead>
        <tr>
          <th>출석</th>
          <th>학생이름</th>
          <th>전화번호</th>
          <th>지각</th>
          <th>조퇴</th>
          <th>결석</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(student, index) in students" :key="index">
          <td>
            <input type="checkbox" v-model="student.attendance" />
          </td>
          <td>{{ student.name }}</td>
          <td>{{ student.phone }}</td>
          <td>
            <input
              type="radio"
              :name="'status-' + index"
              :value="'지각'"
              v-model="student.status"
              @click="toggleRadio(index, '지각')"
            />
          </td>
          <td>
            <input
              type="radio"
              :name="'status-' + index"
              :value="'조퇴'"
              v-model="student.status"
              @click="toggleRadio(index, '조퇴')"
            />
          </td>
          <td>
            <input
              type="radio"
              :name="'status-' + index"
              :value="'결석'"
              v-model="student.status"
              @click="toggleRadio(index, '결석')"
            />
          </td>
        </tr>
      </tbody>
    </v-table>
    <div class="submitAttendance">
      <button @click="submitAttendance">출석 완료</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [
        {
          name: "홍길동",
          phone: "010-1234-5678",
          attendance: false,
          status: null,
        },
        {
          name: "김길동",
          phone: "010-8765-4321",
          attendance: false,
          status: null,
        },
        // 필요한 학생 데이터를 추가하세요.
      ],
    };
  },
  methods: {
    toggleRadio(index, value) {
      if (this.students[index].status === value) {
        this.students[index].status = null;
      }
    },
    submitAttendance() {
      // const attendanceData = this.students.map((student) => ({
      //   name: student.name,
      //   phone: student.phone,
      //   attendance: student.attendance,
      //   status: student.status,
      // }));
      // console.log(attendanceData);
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
  width: 150px;
}

.dashboard-table th {
  background-color: #f4f4f4;
  font-weight: bold;
}

.dashboard-table tr:hover {
  background-color: #f1f1f1;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 20px;
}

button:hover {
  background-color: #0056b3;
}

.submitAttendance {
  display: flex;
  justify-content: flex-end;
}
</style>
