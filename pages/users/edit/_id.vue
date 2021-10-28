<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3>Edit a User</h3>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12" md="9">
        <b-form v-if="show" @submit.prevent="submitForm" @reset="resetForm">
          <b-form-group>
            <b-input
              id="name"
              type="text"
              placeholder="Enter name"
              required
              v-model="form.name">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="username"
              type="text"
              placeholder="Enter username"
              required
              v-model="form.username">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="email"
              type="email"
              placeholder="Enter email"
              required
              v-model="form.email">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="phonenumber"
              type="tel"
              placeholder="Enter a phone number"
              required
              v-model="form.phonenumber">
            </b-input>
          </b-form-group>
          <b-form-group>
            <b-input
              id="password"
              type="password"
              placeholder="Enter password"
              required
              v-model="form.password">
            </b-input>
          </b-form-group>
          <b-row>
            <b-col cols="12" md="2">
              <b-button variant="primary" type="submit">Submit</b-button>
            </b-col>
            <b-col cols="12" md="1">
              <b-button type="reset">Reset</b-button>
            </b-col>
          </b-row>
        </b-form>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      id:'',
      form: {
        name: '',
        username:'',
        email:'',
        phonenumber:'',
        password:''
      },
      show: true
    }
  },

  created() {
    this.id = this.$route.params.id;
    this.getUser();
  },

  methods: {
    getUser() {
      this.$axios.get(`http://localhost:9000/users/${this.id}`).then((response) => {
        this.form = response.data;
        console.log(response.data);
      }).catch((err) => {
        console.log(err);
      })
    },
    submitForm() {
      this.$axios.put(`http://localhost:9000/users/${this.id}`, this.form).then((response) => {
        console.log(response.data);
        this.$router.go(-1);
      }).catch((err) => {
        console.log(err);
      })
    },
    resetForm() {
      this.form.name = ""
      this.form.username = ""
      this.form.email = ""
      this.form.phonenumber = ""
      this.form.password = ""
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 105px;
  }
</style>
