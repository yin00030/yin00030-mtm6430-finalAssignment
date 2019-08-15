<template>
  <div>
    <h1>Dashboard</h1>
    <p>Welcome to your dashboard {{ user.name }}</p>
    <p>Your login email is: {{ user.email }}</p>
    <p>Your age is: {{ user.age }}</p>
    <p>Your job is: {{ user.job }}</p>
    <p>Your city is: {{ user.city }}</p>
    <form @submit.prevent="submitForm">
      <label for="name">Edit your name:</label>
      <input type="text" id="name" v-model="userForm.name" />
      <label for="name">Edit your age:</label>
      <input type="text" id="age" v-model="userForm.age" />
      <label for="name">Edit your city:</label>
      <input type="text" id="city" v-model="userForm.city" />
      <label for="name">Edit your job:</label>
      <input type="text" id="job" v-model="userForm.job" />
      <br />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";
export default {
  data() {
    return {
      userForm: {
        name: "",
        email: "",
        job: "",
        city: "",
        age: ""
      }
    };
  },
  computed: {
    ...mapGetters({
      userData: "getUser"
    }),
    user() {
      return !this.userData ? false : this.userData;
    }
  },
  created() {
    this.getUserData();
  },
  methods: {
    ...mapActions(["fetchUser", "updateUser"]),
    getUserData() {
      let userEmail = localStorage.getItem("userEmail");
      this.fetchUser(userEmail);
    },
    submitForm() {
      const formData = {
        name: this.userForm.name,
        email: this.userForm.email,
        job: this.userForm.job,
        city: this.userForm.city,
        age: this.userForm.age
      };
      this.updateUser(formData);
    }
  }
};
</script>
