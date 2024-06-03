<template>
  <div class="modal-content">
    <h2>강의 등록</h2>
    <div class="lectureForm">
      <div class="left">
        <div class="form-group">
          <label for="subject">강의명</label>
          <input type="text" v-model="form.subject" required />
        </div>
        <div class="form-group">
          <label for="classroom">강의실</label>
          <input type="text" v-model="form.classroom" required />
        </div>
        <div class="form-group">
          <label for="courseName">강의명</label>
          <input type="text" v-model="form.courseName" required />
        </div>
        <div class="form-group">
          <label for="capacity">수강정원</label>
          <input type="text" v-model="form.capacity" required />
        </div>
      </div>
      <div class="right">
        <div class="form-group">
          <label for="contact">연락처</label>
          <input type="text" v-model="form.contact" required />
        </div>
        <div class="form-group">
          <label for="email">이메일</label>
          <input type="email" v-model="form.email" required />
        </div>
        <div class="form-group">
          <label for="startDate">개강일</label>
          <input type="text" v-model="form.startDate" required />
        </div>
        <div class="form-group">
          <label for="endDate">종강일</label>
          <input type="text" v-model="form.endDate" required />
        </div>
      </div>
    </div>
    <div class="form-group">
      <label for="courseDescription">강의소개</label>
      <textarea v-model="form.courseDescription" required></textarea>
    </div>
    <div id="weeksContainer">
      <h3>주차</h3>
      <div v-for="(week, index) in form.weeks" :key="index" class="week-entry">
        <h4>{{ index + 1 }}주차</h4>
        <div class="form-group">
          <label :for="'weekGoal-' + index">학습 목표</label>
          <input
            type="text"
            v-model="week.goal"
            :id="'weekGoal-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'weekContent-' + index">학습 내용</label>
          <textarea
            v-model="week.content"
            :id="'weekContent-' + index"
            required
          ></textarea>
        </div>
      </div>
    </div>
    <div class="form-buttons">
      <button type="button" @click="addWeek" class="addWeek-button">
        주차추가
      </button>
      <button type="button" @click="removeWeek" class="removeWeek-button">
        주차삭제
      </button>
    </div>
    <div class="form-button2">
      <template v-if="paction === 'U'">
        <button type="button" class="insert-button">강의수정</button>
      </template>
      <template v-else
        ><button type="button" class="insert-button">강의등록</button></template
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    action: String,
  },
  data() {
    return {
      form: {
        subject: "",
        classroom: "",
        courseName: "",
        capacity: "",
        contact: "",
        email: "",
        startDate: "",
        endDate: "",
        courseDescription: "",
        weeks: [],
      },
      paction: this.action,
    };
  },
  methods: {
    addWeek() {
      this.form.weeks.push({ goal: "", content: "" });
    },
    removeWeek() {
      if (this.form.weeks.length > 0) {
        this.form.weeks.pop();
      } else {
        alert("더 이상 삭제할 주차가 없습니다.");
      }
    },
  },
};
</script>

<style scoped>
.lectureForm {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.modal-content {
  background-color: #fefefe;
  padding: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  animation: animatetop 0.4s;
}

@keyframes animatetop {
  from {
    top: -300px;
    opacity: 0;
  }
  to {
    top: 0;
    opacity: 1;
  }
}

.close-button {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close-button:hover,
.close-button:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #dfdfdf;
}

.form-buttons {
  margin-top: 20px;
  display: flex;
  justify-content: flex-end;
}

.form-buttons button {
  margin-right: 10px;
}

.form-button2 {
  display: flex;
  justify-content: flex-end;
  position: relative;
  top: 10px;
  right: 10px;
}

#weeksContainer {
  margin-top: 20px;
}

.week-entry {
  margin-bottom: 20px;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 5px;
}

.insert-button,
.addWeek-button {
  padding: 10px 17px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.insert-button:hover,
.addWeek-button:hover {
  background-color: #0056b3;
}

.removeWeek-button {
  padding: 10px 17px;
  background-color: #d32f2f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.removeWeek-button:hover {
  background-color: #e57373;
  box-shadow: 0 4px 8px rgba(211, 47, 47, 0.2);
}
</style>
