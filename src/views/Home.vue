<template>
  <div class="home">
    <div>
      <div v-for="student in students" v-bind:key="student.id">
        <div class="card">
          <div class="title_bar">
            <h1>{{ student.firstName + " " + student.lastName }}</h1>
            <button>+</button>
          </div>
          <div class="content">
            <img class="avatar" :src="student.pic" />
            <ul>
              <p>Email: {{ student.email }}</p>
              <p>Company: {{ student.company }}</p>
              <p>Skill: {{ student.skill }}</p>
              <p>Average: {{ student.average }}</p>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
text {
  font-family: Raleway;
}
.card {
  text-align: left;
  flex-direction: column;
  display: flex;
  justify-content: flex;
  width: 60%;
}
.title_bar {
  background: #507818;
  border-radius: 10px;
  border: rounded;

  display: flex;
  justify-content: flex;

  align-items: center;
  align-self: stretch;
}

.content {
  display: flex;
  align-items: center;
  align-self: center;
}
.avatar {
  width: 10vw;
  height: 10vw;
  align-self: center;
  border: 2px solid black;
  border-radius: 50%;
}
</style>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  data: function () {
    return {
      students: [],
    };
  },
  created: function () {
    this.indexStudents();
  },
  methods: {
    indexStudents: function () {
      axios.get("https://api.hatchways.io/assessment/students").then((response) => {
        //console.table(response.data.students);
        this.students = response.data.students;
        let imageLinks = [];
        //average grades
        this.students.forEach((student) => {
          let mean = student.grades.reduce((a, b) => parseInt(a) + parseInt(b), 0) / student.grades.length;
          student.average = mean;
          //image variable
          imageLinks.push(student.pic);
        });
      });
    },
  },
};
</script>
