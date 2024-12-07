<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'

// Bước 1: Khai báo 1 biến để lưu dữ liệu lấy về từ API. Kiểu dữ liệu của biến là kiểu mảng
// Bước 2: Khai báo 1 hàm lấy dữ liệu và sau đó lưu dữ liệu vào BƯỚC 1
// Bước 3: Sử dụng vầo lặp để hiển thị dữ liệu ra bảng

// Bước 1
let studentList = ref([])

// Bước 2
let fetchStudents = async () => {
  // Khai báo 1 biến để lưu dữ liệu lấy đc từ API
  let response = await axios.get('http://localhost:3000/students')
  // Lưu dữ liệu lấy đc từ API vào mảng studentList
  studentList.value = response.data
}

fetchStudents()

// Chức năng xoá
let handleDelete = async (id) => {
  let confirmDelete = confirm('Bạn có muốn xoá không ?')

  if (!confirmDelete) return
  // Gọi hàm API để xoá dữ liệu
  await axios.delete(`http://localhost:3000/students/${id}`)
  // Sau khi xoá xong gọi hàm fetchStudent để cập nhật lại dữ liệu cho bảng
  fetchStudents()
}
</script>

<template>
  <main>
    <h1 class="text-bold">Student List</h1>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <RouterLink class="btn btn-primary" :to="`/students/add`">Add</RouterLink>
        </div>
        <div class="col-md-12">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Name</th>
                <th scope="col">Age</th>
                <th scope="col">Email</th>
                <th scope="col">Image</th>
                <th scope="col">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="student in studentList">
                <th scope="row">{{ student.id }}</th>
                <td>{{ student.name }}</td>
                <td>{{ student.age }}</td>
                <td>{{ student.email }}</td>
                <td><img :src="student.image" alt="" /></td>
                <td>
                  <button class="btn btn-danger" @click="handleDelete(student.id)">Delete</button>
                  <RouterLink class="btn btn-primary" :to="`/students/detail/${student.id}`"
                    >Detail</RouterLink
                  >
                  <RouterLink class="btn btn-warning" :to="`/students/edit/${student.id}`"
                    >Edit</RouterLink
                  >
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </main>
</template>
