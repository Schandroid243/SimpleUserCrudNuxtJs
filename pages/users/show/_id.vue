<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3>User Details</h3>
    </b-row>
    <b-row align-h="end" class="listButton">
      <b-button @click="goBack" variant="primary">
        List of User
      </b-button>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12" md="9">
        <div>
          <div>
            <span>Name: </span>
            <span>{{form.name}}</span>
          </div>
          <div>
            <span>Username: </span>
            <span>{{form.username}}</span>
          </div>
          <div>
            <span>Email: </span>
            <span>{{form.email}}</span>
          </div>
          <div>
            <span>PhoneNumber: </span>
            <span>{{form.phonenumber}}</span>
          </div>
        </div>
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
      form:{
        name:'',
        username:'',
        email:'',
        phonenumber:''
      }
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
    goBack() {
      this.$router.go(-1);
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 45px;
  }
  .listButton {
    margin-right: 50px;
  }
</style>
