<template>
  <h1>Edit Student</h1>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
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

          <button class="btn btn-primary" type="submit">Sửa</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'
import router from '@/router'

// Bước 1
let { params } = useRoute()

// Bước 2
let student = ref({
  name: '',
  age: '',
  email: '',
  image: '',
})

// Bước 3

let handleSubmit = async () => {
  // Gọi API sửa dữ liệu
  await axios.put(`http://localhost:3000/students/${params.id}`, student.value)
  // Sau khi sửa xong thì điều hướng người dùng về trang danh sách
  router.push({ name: 'home' })
}

let fetchStudent = async () => {
  let response = await axios.get(`http://localhost:3000/students/${params.id}`)
  student.value = response.data
}

fetchStudent()
</script>

<style lang="scss" scoped></style>
