<template>
  <div class="home">
    <div>
      <ul>
        BUTTS
        <li v-for="student in students" v-bind:key="student.id">{{ student }}</li>
      </ul>
    </div>
  </div>
</template>

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
      });
    },
  },
};
</script>
