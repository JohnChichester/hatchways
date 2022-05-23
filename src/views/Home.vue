<template>
  <div class="home">
    <div>
      <div v-for="student in students" v-bind:key="student.id">
        <div id="block_container">
          <div>
            <img :src="student.pic" />
          </div>

          <ul>
            <h1>{{ student.firstName + " " + student.lastName }}</h1>
            <p>Email: {{ student.email }}</p>
            <p>Company: {{ student.company }}</p>
            <p>Skill: {{ student.skill }}</p>
            <p>Average: {{ student.average }}</p>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
#avatar {
  border-radius: ;
}
#block_container {
  font: Raleway;
  text-align: left;
  display: flex;
  justify-content: center;
  align-items: center;
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
