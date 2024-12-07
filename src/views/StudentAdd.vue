<template>
  <h1>Add Student</h1>
  <!-- sử dụng @submit.prevent để chặn lại việc tải trang khi ấn nút thêm -->
  <form @submit.prevent="handleSubmit">
    <div class="mb-3">
      <label for="exampleFormControlInput1" class="form-label">Name</label>
      <input
        type="text"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Nhập tên..."
        v-model="student.name"
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput1" class="form-label">Age</label>
      <input
        type="number"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Nhập tuổi..."
        v-model="student.age"
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput1" class="form-label">Email</label>
      <input
        type="email"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Nhập email..."
        v-model="student.email"
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput1" class="form-label">Link ảnh</label>
      <input
        type="text"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Nhập link ảnh..."
        v-model="student.image"
      />
    </div>

    <button class="btn btn-primary" type="submit">Thêm mới</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import router from '@/router'
import axios from 'axios'
// Bước 1: Khai báo 1 biến để lưu dữ liệu người dùng nhập vào
// Bước 2: Khai báo 1 hàm để gọi API và lưu dữ liệu lên CSDL

// Bước 1
let student = ref({
  name: '',
  age: '',
  email: '',
  image: '',
})

let handleSubmit = async () => {
  // Gọi API để dữ liệu người dùng nhập vào
  await axios.post('http://localhost:3000/students/', student.value)

  router.push({ name: 'home' })
}
</script>

<style lang="scss" scoped></style>
