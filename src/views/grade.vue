<template>
  <div class="outer-container">
    <div class="container">
      <h1>ตรวจสอบคะแนนและแสดงเกรด</h1>
      <div class="form-group">
        <label for="score">กรอกคะแนนของคุณ:</label>
        <input v-model="score" type="number" id="score" min="0" max="100" />
      </div>
      <button @click="checkGrade" class="btn">ตรวจสอบเกรด</button>
      <div v-if="grade !== null" class="result">
        <h2>เกรดของคุณคือ: {{ grade }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";
export default {
  data() {
    return {
      score: null,
      grade: null
    };
  },
  methods: {
    checkGrade() {
      const score = this.score;
      if (score >= 80) {
        this.grade = 'A';
        Swal.fire({
                title: (this.grade),
                text: "เกรดของคุณคือ: " + this.grade,
                icon: "success"
        });
        
      } else if (score >= 70) {
        this.grade = 'B';
        Swal.fire({
                title: (this.grade),
                text: "เกรดของคุณคือ: " + this.grade,
                icon: "success"
        });
      } else if (score >= 60) {
        this.grade = 'C';
        Swal.fire({
                title: (this.grade),
                text: "เกรดของคุณคือ: " + this.grade,
                icon: "success"
        });
      } else if (score >= 50) {
        this.grade = 'D';
        Swal.fire({
                title: (this.grade),
                text: "เกรดของคุณคือ: " + this.grade,
                icon: "success"
        });
      } else {
        this.grade = 'F';
        Swal.fire({
                title: (this.grade),
                text: "เกรดของคุณคือ: " + this.grade,
                icon: "error"
        });
      }
    }
  }
};
</script>


<style scoped>
.outer-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  font-family: Arial, sans-serif;
  background-color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  border: 2px solid #4CAF50;
}

h1 {
  color: #4CAF50;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-size: 18px;
  margin-bottom: 10px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.btn {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 18px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn:hover {
  background-color: #45a049;
}

.result {
  margin-top: 20px;
}

h2 {
  font-size: 24px;
  color: #333;
}
</style>
