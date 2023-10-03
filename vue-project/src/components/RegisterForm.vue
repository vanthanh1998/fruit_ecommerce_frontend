<template>
  <div class="p-5">
    <form @submit.prevent="register" class="form-signin">
      <h2 class="mb-3">Register</h2>
      <input
        v-model="name"
        type="text"
        class="form-control mb-2"
        placeholder="Name"
        autofocus
      />
      <div v-if="errors && errors.name" class="text-danger mb-2">
        {{ errors.name[0] }}
      </div>

      <input
        v-model="email"
        type="email"
        class="form-control mb-2"
        placeholder="Email"
      />
      <div v-if="errors && errors.email" class="text-danger mb-2">
        {{ errors.email[0] }}
      </div>

      <input
        v-model="password"
        type="password"
        class="form-control mb-2"
        placeholder="Password"
      />
      <div v-if="errors && errors.password" class="text-danger mb-2">
        {{ errors.password[0] }}
      </div>

      <button class="btn btn-lg btn-primary btn-block" type="submit">
        Register
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
      errors: {},
    };
  },
  methods: {
    async register() {
      if (!this.passwordMismatch) {
        const userData = {
          name: this.name,
          email: this.email,
          password: this.password,
        };

        try {
          const response = await axios.post(
            `${import.meta.env.VITE_API_URL}register`,
            userData
          );
          console.log(response.data);
        } catch (error) {
          if (error.response && error.response.data.errors) {
            this.errors = error.response.data.errors;
          } else {
            console.error("There was an error registering the user:", error);
          }
        }
      }
    },
  },
};
</script>
