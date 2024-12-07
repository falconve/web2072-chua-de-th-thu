<script setup>
// Bước 1: lấy id từ thanh url sử dụng useRoute()
// Bước 2: Khai báo biến kiểu dữ liệu là object để lưu dữ liệu lấy từ API
// Bước 3: Khai báo hàm để gọi API

import { ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

// Bước 1
let { params } = useRoute()

// Bước 2
let student = ref({})

// Bước 3
let fetchStudent = async () => {
  let response = await axios.get(`http://localhost:3000/students/${params.id}`)
  student.value = response.data
}

fetchStudent()
</script>

<template>
  <h1>Student Detail</h1>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="card" style="width: 18rem">
          <img :src="student.image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">ID: {{ student.id }}</h5>
            <p class="card-text">Name: {{ student.name }}</p>
            <p class="card-text">Age: {{ student.age }}</p>
            <p class="card-text">Email: {{ student.email }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
