<template >
  <div>
    <div class="container mt-4 align-items-center">
      <input
        type="text"
        class="form-control w-50 d-inline mb-3 rounded-pill"
        v-model="name"
      />
      <input
        type="submit"
        class="btn btn-primary mb-2 mx-3 w-25 rounded-pill"
        @click="addNew"
        value="ADD"
      />

      <ul class="list-group">
        <li class="list-group-item bg-dark text-white" v-for="user in users" :key="user.id">
          {{ user.name }}
          <span class="float-right" @click="removeNames"> <i class="far fa-trash-alt"></i> </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
/* eslint-disable */

import axios from "axios";

export default {
  data() {
    return {
      users: [],
      addedName: null
    };
  },
  async created() {
    let fetchUsers = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );
    this.users = fetchUsers.data;
  },
  methods: {
    addNew() {
      if (this.addedName === "") {
        alert("Enter A valid Name");
      } else {
        let i_d = this.users.length + 1;
        let user = ({ id: i_d, name: this.name });
        this.users.unshift(user);
        this.name = "";
      }
    },
    removeNames(name) {
      let currentName = this.users.indexOf(name);
      this.users.splice(this.currentName, 1);
    }
  }
};
</script>
