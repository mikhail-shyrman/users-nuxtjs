<template>
  <div>
    <v-breadcrumbs :items="items">
      <template v-slot:divider>
        <v-icon>mdi-chevron-right</v-icon>
      </template>
    </v-breadcrumbs>
    <v-row>
      <v-col cols="12" lg="4" md="6" sm="12">
        <v-card
            class="mx-auto"
            max-width="344"
            outlined
        >
          <v-list-item three-line>
            <v-list-item-content>
              <div class="overline mb-4">
                {{ user.data.email }}
              </div>
              <v-list-item-title class="headline mb-1">
                {{ user.data.first_name }} {{ user.data.last_name }}

              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-avatar
                tile
                size="80"
                color="grey"
            >
              <img
                  alt="user"
                  :src="user.data.avatar"
              >
            </v-list-item-avatar>
          </v-list-item>

        </v-card>
      </v-col>
      <v-col cols="12" lg="8" md="6" sm="12">
        <v-alert
            border="left"
            color="indigo"
            dark
        >
          Some kind of information
        </v-alert>
      </v-col>
    </v-row>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    user: {
      data: []
    },
    items: [
      {
        text: "Users",
        disabled: false,
        href: "/users"
      },
      {
        text: "Users details",
        disabled: true,
        href: "user"
      }
    ]
  }),
  methods: {
    getUser () {
      axios.get("https://reqres.in/api/users/" + this.$route.params.id
      ).then(response => {
        this.user = response.data;
      });
    }
  },
  mounted () {
    this.getUser();
  }
};
</script>