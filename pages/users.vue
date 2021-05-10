<template>
  <div>
    <v-row>
      <v-col cols="12" lg="4" md="6" sm="12" v-for="(user, key) in users.data" :key="key">
        <v-card
            class="mx-auto"
            max-width="344"
            outlined
        >
          <v-list-item three-line>
            <v-list-item-content>
              <div class="overline mb-4">
                {{ user.email }}
              </div>
              <v-list-item-title class="headline mb-1">
                {{ user.first_name }} {{ user.last_name }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-avatar
                tile
                size="80"
                color="grey"
            >
              <img
                  alt="user"
                  :src="user.avatar"
              >
            </v-list-item-avatar>
          </v-list-item>
          <v-card-actions>
            <v-btn
                :to="'/user/'+ user.id"
                outlined
                rounded
                text
            >
              Details
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <div class="text-center" v-if="users.total_pages">
          <v-pagination
              v-model="page"
              :length="users.total_pages"
              :total-visible="7"
              @input="handlePageChange"
          ></v-pagination>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    page: 1,
    users: {
      page: "",
      per_page: "",
      total_pages: "",
      data: []
    }
  }),
  methods: {
    handlePageChange (value) {
      this.page = value;
      this.getUsers();
    },
    getUsers () {
      axios.get("https://reqres.in/api/users?&page=" + this.page
      ).then(response => {
        this.users = response.data;
      });
    }
  },
  mounted () {
    this.getUsers();
  }
};
</script>

