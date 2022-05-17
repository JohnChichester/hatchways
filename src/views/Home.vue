<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
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
