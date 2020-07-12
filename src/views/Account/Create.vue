<template>
  <div id="account-create">
    <v-text-field
      label="email"
      single-line
      outlined
      v-model="email"
    ></v-text-field>
    <v-text-field
      label="password"
      single-line
      outlined
      v-model="password"
    ></v-text-field>
    <v-btn @click="signUp">登録する</v-btn>
  </div>
</template>

<script>
import { Auth } from "aws-amplify";

export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    signUp: async function() {
      const { email, password } = this;
      try {
        const user = await Auth.signUp({
          username: email,
          password,
          attributes: {
            email
          }
        });
        console.log({ user });
      } catch (error) {
        console.log("error signing up:", error);
      }
    }
  }
};
</script>
