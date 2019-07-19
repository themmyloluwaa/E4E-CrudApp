<template>
  <div id="app">
    <h1 class="h1">Ehealth4Everyone Attendance App</h1>
    <AddVisitors v-on:add-user="addUser" />
    <VisitorList v-bind:visitors="visitorInfo" class="header" v-on:onDelete="deleteVisitor" />
   
  </div>
</template>

<script>
import AddVisitors from "./components/AddVisitors.vue";
import VisitorList from "./components/VisitorList";

export default {
  name: "app",
  components: { VisitorList, AddVisitors },
  data() {
    return {
      visitorInfo: []
    };
  },
  methods: {
    addUser(inputData) {
      this.visitorInfo = [...this.visitorInfo, inputData];
    },
    deleteVisitor(id) {
      this.visitorInfo = this.visitorInfo.filter(e => e.id !== id);
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  line-height: 1.4;
}
#app {
  background-color: #013033;
  min-height: 100vh;
  scroll-behavior: none;
  color: rgb(246, 245, 245);
  overflow: hidden;
}
.h1 {
  text-align: center;
  margin: 20px 0;
}

@media screen and (max-width: 400px) {
  #app {
    font-size: 15px;
  }
}
</style>
