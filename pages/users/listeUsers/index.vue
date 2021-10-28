<template>
  <b-container>
    <b-row class="d-flex justify-content-center rowTitle">
      <h3>Liste of User</h3>
    </b-row>
    <b-row align-h="end">
      <b-link :to="{name: 'users-add'}">
        <b-button variant="primary" class="addUserButton"> Create user </b-button>
      </b-link>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12" md="9">
        <b-table
          id="userTable"
          :fields="fields"
          :items="listeUser"
          :per-page="perPage"
          :current-page="currentPage"
          striped
          class="userTable"
          responsive="sm">

            <col v-for="(user, i) in listeUser" :key="i">
            <template #cell(Name)="user">{{user.item.name}}</template>
            <template #cell(Username)="user">{{user.item.username}}</template>
            <template #cell(Email)="user">{{user.item.email}}</template>
            <template #cell(PhoneNumber)="user">{{user.item.phonenumber}}</template>

            <template #cell(Action)="user">
              <b-row>
                <b-col cols="8" md="4">
                  <b-link :to="{name: 'users-edit-id', params:{id: user.item._id}}">
                    <b-button variant="warning">
                      <b-icon icon="pencil-fill"></b-icon>
                    </b-button>
                  </b-link>
                </b-col>
                <b-col cols="8" md="4">
                  <b-link :to="{name: 'users-show-id', params:{id: user.item._id}}">
                    <b-button variant="primary">
                      <b-icon icon="info-circle-fill"></b-icon>
                    </b-button>
                  </b-link>
                </b-col>
                <b-col cols="8" md="4">
                    <b-button variant="danger" @click="delUser(user.item._id)">
                      <b-icon icon="trash-fill"></b-icon>
                    </b-button>
                </b-col>
              </b-row>
            </template>
          </b-table>
          <b-pagination
            id="pagination"
            v-model="currentPage"
            :per-page="perPage"
            :total-rows="rows"
            aria-controls="userTable">
          </b-pagination>
      </b-col>
    </b-row>
  </b-container>
</template>
<script lang="ts">
import Vue from 'vue'
import { BootstrapVueIcons } from 'bootstrap-vue'

Vue.use(BootstrapVueIcons);
export default Vue.extend({
  data() {
    return {
      perPage: 4,
      currentPage: 1,
      listeUser: [],
      fields: [
        "Name",
        "Username",
        "Email",
        "PhoneNumber",
        "Action"
      ],
    }
  },

  mounted() {
    this.getUser();
  },

  methods: {
    getUser() {
      this.$axios.get(`http://localhost:9000/users/`).then((response) => {
        this.listeUser = response.data;
        console.log(response.data);
      }).catch((err) => {
        console.log(err);
      })
    },
    delUser(userId: Text) {
      this.$axios.delete(`http://localhost:9000/users/${userId}`).then((response) => {
        console.log(response.data);
        this.getUser();
      }).catch((err) => {
        console.log(err);
      })
    }
  },
  computed: {
    rows(): number {
      return this.listeUser.length;
    }
  }
})
</script>
<style scoped>
  .rowTitle {
    margin-top: 70px;
  }
  .userTable {
    margin-top: 30px;
  }
  .addUserButton {
    margin-right: 45px;
  }
</style>
