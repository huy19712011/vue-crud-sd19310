<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import { ref } from "vue";

const students = ref([
  {
    id: 1,
    name: "student 1",
    course: "course 1",
    email: "email 1",
    phone: "phone 1",
    created_at: "2024-10-17",
    updated_at: "2024-10-18",
  },
  {
    id: 2,
    name: "student 2",
    course: "course 2",
    email: "email 2",
    phone: "phone 2",
    created_at: "2024-10-17",
    updated_at: "2024-10-18",
  },
  {
    id: 3,
    name: "student 3",
    course: "course 3",
    email: "email 3",
    phone: "phone 3",
    created_at: "2024-10-17",
    updated_at: "2024-10-18",
  },
]);

const model = ref({
  student: {
    name: "",
    course: "",
    email: "",
    phone: "",
  },
});

const saveStudent = () => {
  students.value.push({
    id: students.value.length + 1,
    name: model.value.student.name,
    course: model.value.student.course,
    email: model.value.student.email,
    phone: model.value.student.phone,
    created_at: new Date().toISOString().split("T")[0],
    updated_at: new Date().toISOString().split("T")[0],
  });
};
</script>

<template>
  <header>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <RouterLink
          class="navbar-brand"
          to="/"
          >Navbar
        </RouterLink>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div
          class="collapse navbar-collapse"
          id="navbarSupportedContent"
        >
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <RouterLink
                class="nav-link active"
                aria-current="page"
                to="/"
                >Home
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink
                class="nav-link active"
                aria-current="page"
                to="/about"
                >About
              </RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink
                class="nav-link active"
                aria-current="page"
                to="/students"
                >Students
              </RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
  <body>
    <div class="card">
      <div class="card-header">
        <h4>Add Student</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">Name</label>
          <input
            type="text"
            class="form-control"
            v-model="model.student.name"
          />
        </div>
        <div class="mb-3">
          <label for="">Course</label>
          <input
            type="text"
            class="form-control"
            v-model="model.student.course"
          />
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input
            type="text"
            class="form-control"
            v-model="model.student.email"
          />
        </div>
        <div class="mb-3">
          <label for="">Phone</label>
          <input
            type="text"
            class="form-control"
            v-model="model.student.phone"
          />
        </div>
        <div class="mb3">
          <button
            type="button"
            class="btn btn-primary"
            @click="saveStudent"
          >
            Save
          </button>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="card">
        <div class="card-header">
          <h4>
            Students
            <RouterLink
              to="/students/create"
              class="btn btn-primary float-end"
              >Add Student
            </RouterLink>
          </h4>
        </div>
        <div class="card-body">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Course</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Created at</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(student, index) in students"
                :key="student.id"
              >
                <td>{{ student.id }}</td>
                <td>{{ student.name }}</td>
                <td>{{ student.course }}</td>
                <td>{{ student.email }}</td>
                <td>{{ student.phone }}</td>
                <td>{{ student.created_at }}</td>
                <td>
                  <RouterLink
                    class="btn btn-success"
                    :to="{ path: '/students/' + student.id + '/edit' }"
                    @click="editStudent(student)"
                  >
                    Edit
                  </RouterLink>
                  <RouterLink
                    class="btn btn-danger"
                    to="/"
                  >
                    Delete
                  </RouterLink>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </body>
</template>
