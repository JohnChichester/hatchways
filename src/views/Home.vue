<template>
  <div class="home">
    <div>
      <div v-for="student in students" v-bind:key="student.id">
        <img :scr="student.pic" />
        <h1>{{ student.firstName + " " + student.lastName }}</h1>
        <p>Email: {{ student.email }}</p>
        <p>Company: {{ student.company }}</p>
        <p>Skill: {{ student.skill }}</p>
        <p>Average: {{ student.average }}%</p>
      </div>
    </div>
  </div>
</template>

<style></style>

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
        //average grades
        this.students.forEach((student) => {
          let mean = student.grades.reduce((a, b) => parseInt(a) + parseInt(b), 0) / student.grades.length;
          student.average = mean;
        });
      });
    },
  },
};
</script>
