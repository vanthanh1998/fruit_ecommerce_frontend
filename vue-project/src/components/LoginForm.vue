<template>
  <div class="p-5">
    <form @submit.prevent="login" class="form-signin">
      <h2 class="mb-3">Login</h2>
      <input
        v-model="email"
        type="email"
        class="form-control mb-2"
        placeholder="Email"
        required
        autofocus
      />
      <input
        v-model="password"
        type="password"
        class="form-control mb-3"
        placeholder="Password"
        required
      />
      <button class="btn btn-lg btn-primary btn-block" type="submit">
        Sign in
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      console.log("Email:", this.email, "Password:", this.password);
    },
  },
};
</script>
