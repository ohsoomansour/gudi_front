<template>
  <div class="lecture-detail">
    <h2 class="title">공지사항</h2>
    <!-- <p class="content">Content: {{ content }}</p> -->
    <div class="form-group">
      <div class="form-label">제목</div>
      <input type="text" name="content" class="form-input" />
    </div>
    <div class="form-group">
      <div class="form-label">내용</div>
      <input type="text" name="content" class="form-input" />
    </div>
    <div class="form-group">
      <div class="form-label">작성자</div>
      <input type="text" name="content" class="form-input" />
    </div>
    <div class="form-group">
      <div class="form-label">등록일</div>
      <input type="text" name="content" class="form-input" />
    </div>
    <div class="button-group">
      <button class="delete-button">삭제</button>
      <button class="update-button">저장</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    content: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.lecture-detail {
  padding: 16px;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  margin-top: 16px;
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

.form-input {
  padding: 10px;
  border: 1px solid #dcdcdc;
  border-radius: 4px;
  font-size: 14px;
  color: #34495e;
}

.form-input:focus {
  border-color: #407bff;
  box-shadow: 0 0 4px rgba(64, 123, 255, 0.2);
  outline: none;
}

.button-group {
  display: flex;
  justify-content: flex-end;
}

.update-button {
  padding: 10px 16px;
  background-color: #407bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-left: 8px;
}

.update-button:hover {
  background-color: #5a9bff;
  box-shadow: 0 4px 8px rgba(64, 123, 255, 0.2);
}

.delete-button {
  padding: 10px 16px;
  background-color: #d32f2f;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-left: 8px;
}

.delete-button:hover {
  background-color: #e57373;
  box-shadow: 0 4px 8px rgba(211, 47, 47, 0.2);
}
</style>
