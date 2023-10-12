<template>
    <v-container fluid>
      <v-row justify="center">
        <v-col cols="12" sm="8" md="6">
          <v-card>
            <v-card-title class="headline"> Login </v-card-title>
            <v-card-text>
              <v-form @submit.prevent="login">
                <v-text-field
                  v-model="formData.username"
                  label="Username"
                  required
                ></v-text-field>
                <v-text-field
                  v-model="formData.password"
                  label="Password"
                  type="password"
                  required
                ></v-text-field>
                <v-btn color="primary" type="submit">Login</v-btn>
              </v-form>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
  name: 'LoginView',
    data() {
      return {
        formData: {
          username: "",
          password: "",
        },
      };
    },
    methods: {
      login() {
        // Here you can add your login logic
        // For simplicity, we'll just log the form data
        console.log("Login Data:", this.formData);
      },
    },
  };
  </script>