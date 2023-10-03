<template>
  <div class="p-5">
    <form @submit.prevent="loginForm" class="form-signin">
      <h2 class="mb-3">Login</h2>
      <input
        v-model="email"
        type="email"
        class="form-control mb-2"
        placeholder="Email"
        autofocus
      />
      <div v-if="errors && errors.email" class="text-danger mb-2">
        {{ errors.email[0] }}
      </div>

      <input
        v-model="password"
        type="password"
        class="form-control mb-3"
        placeholder="Password"
      />
      <div v-if="errors && errors.password" class="text-danger mb-2">
        {{ errors.password[0] }}
      </div>

      <button class="btn btn-lg btn-primary btn-block" type="submit">
        Sign in
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";

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
    async loginForm() {
      if (!this.passwordMismatch) {
        const userData = {
          email: this.email,
          password: this.password,
        };

        try {
          const response = await axios.post(
            `${import.meta.env.VITE_API_URL}login`,
            userData
          );
          console.log(response.data);

          // sucess
          Swal.fire({
            icon: "success",
            title: "Đăng nhập thành công",
            text: "Chào mừng bạn quay trở lại!",
            timer: 1500,
          }).then(() => {
            this.$router.push("/");
          });
        } catch (error) {
          if (error.response && error.response.data.errors) {
            this.errors = error.response.data.errors;
          } else {
            console.error("There was an error login the user:", error);
          }
        }
      }
    },
  },
};
</script>
