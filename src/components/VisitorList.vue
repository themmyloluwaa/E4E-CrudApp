<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Address</th>
          <th scope="col">Comment</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(visitor,index) in visitors" v-bind:key="visitor.id">
          <th scope="row">
            <input v-if="status[index]" v-model="visitor.name" />
            <span v-if="!status[index]">{{visitor.name}}</span>
          </th>
          <td>
            <input v-if="status[index]" v-model="visitor.email" />
            <span v-if="!status[index]">{{visitor.email}}</span>
          </td>
          <td>
            <input v-if="status[index]" v-model="visitor.address" />
            <span v-if="!status[index]">{{visitor.address}}</span>
          </td>
          <td>
            <input v-if="status[index]" v-model="visitor.comment" />
            <span v-if="!status[index]">{{visitor.comment}}</span>
          </td>
          <td>
            <div>
              <b-button
                v-if="!status[index]"
                class="btn-style"
                variant="warning"
                @click="reRender(visitor,true,index)"
              >Edit</b-button>
              <!-- THe onUpdate event will update the userInfo of the parent component -->
              <b-button
                v-if="status[index]"
                class="btn-style"
                variant="success"
                @click="reRender(visitor,false,index)"
              >Update</b-button>
              <b-button
                v-if="status[index]"
                class="btn-style btn-color"
                @click="reRender(visitor,false,index)"
              >Cancel</b-button>
              <b-button
                v-if="!status[index]"
                @click="$emit('onDelete', visitor.id)"
                class="btn-style btn-color"
              >Delete</b-button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "VisitorList",
  props: ["visitors"],
  data() {
    return {
      status: null
    };
  },
  methods: {
    reRender(user, state, index) {
      this.status[index] = state;
      //Make it rerender
      user.id += 100;
    },
    closeBtn(state, index) {
      this.status[index] = state;
    }
   
  },
  created() {
    //Set status to an array with the length of users
    this.status = new Array(this.$props.visitors.length).fill(false);
  },
  computed: {
    users() {
      //Get the user from props, so that we can watch for it
      return this.$props.visitors;
    }
  },
  watch: {
    users() {
      //Anytime a new user is created, push false to the array
      this.status.push(false);
    }
  }
};
</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.css");
table {
  border: 1px solid black;
  border-radius: 1em;
  table-layout: fixed;
  width: 80vw;
  margin: 0 auto;
  background: rgb(119, 117, 117);
  color: #fff;
  overflow: hidden;
  margin-top: 20px;
}

th,
td {
  border: 1px solid rgb(255, 251, 251);
  min-width: 100px;
  overflow: hidden;
  word-wrap: break-word;
  font-size: 0.8em;
}
thead {
  font-size: 1.5em;
  text-align: center;
}

.btn-style {
  margin: 0 10px;
  color: #000;
}
.btn-color {
  background: rgb(255, 251, 251);
}
.btn-color:hover {
  background: rgb(231, 9, 9);
}
input {
  height: 30px;
  border-radius: 5px;
  /* text-align: center; */
  padding: 10px;
}
</style>

