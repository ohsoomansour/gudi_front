<template>
  <div class="modal-content">
    <h2>시험 출제</h2>
    <div class="form-group">
      <label for="examName">시험명</label>
      <input type="text" v-model="form.examName" required />
    </div>

    <div id="questionsContainer">
      <!-- <h3>문제</h3> -->
      <div
        v-for="(question, index) in form.questions"
        :key="index"
        class="question-entry"
      >
        <h4>문제 {{ index + 1 }}</h4>
        <div class="form-group">
          <!-- <label :for="'question-' + index">문제</label> -->
          <input
            type="text"
            v-model="question.question"
            :id="'question-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'option1-' + index">보기1</label>
          <input
            type="text"
            v-model="question.option1"
            :id="'option1-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'option2-' + index">보기2</label>
          <input
            type="text"
            v-model="question.option2"
            :id="'option2-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'option3-' + index">보기3</label>
          <input
            type="text"
            v-model="question.option3"
            :id="'option3-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'option4-' + index">보기4</label>
          <input
            type="text"
            v-model="question.option4"
            :id="'option4-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'answer-' + index">정답</label>
          <input
            type="text"
            v-model="question.answer"
            :id="'answer-' + index"
            required
          />
        </div>
        <div class="form-group">
          <label :for="'score-' + index">배점</label>
          <input
            type="number"
            v-model="question.score"
            :id="'score-' + index"
            required
          />
        </div>
      </div>
    </div>
    <div class="form-buttons">
      <button @click="addQuestion" class="addQuestion-button">문제추가</button>
      <button @click="removeQuestion(index)" class="removeQuestion-button">
        문제삭제
      </button>
    </div>

    <div class="form-buttons">
      <template v-if="paction === 'U'">
        <button type="button" class="update-button">시험수정</button>
        <button type="button" class="delete-button">시험삭제</button>
      </template>
      <template v-else
        ><button type="button" class="insert-button">시험등록</button></template
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
        examName: "",
        examDescription: "",
        questions: [],
      },
      paction: this.action,
    };
  },
  methods: {
    addQuestion() {
      this.form.questions.push({
        question: "",
        option1: "",
        option2: "",
        option3: "",
        option4: "",
        answer: "",
        score: 0,
      });
    },
    removeQuestion(index) {
      if (this.form.questions.length > 0) {
        this.form.questions.splice(index, 1);
      } else {
        alert("더 이상 삭제할 문제가 없습니다.");
      }
    },
    save() {},
  },
};
</script>

<style scoped>
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
  margin-top: 10px;
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

#questionsContainer {
  margin-top: 20px;
}

.question-entry {
  margin-bottom: 20px;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 5px;
}

.insert-button,
.update-button,
.addQuestion-button {
  padding: 10px 17px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.insert-button:hover,
.update-button:hover,
.addQuestion-button:hover {
  background-color: #0056b3;
}

.removeQuestion-button,
.delete-button {
  padding: 10px 17px;
  background-color: #d32f2f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.removeQuestion-button:hover,
.delete-button:hover {
  background-color: #e57373;
  box-shadow: 0 4px 8px rgba(211, 47, 47, 0.2);
}
</style>
