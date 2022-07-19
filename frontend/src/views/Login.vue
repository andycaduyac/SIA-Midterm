<template>
<div class="container mt-5 w-25 border rounded p-2">
  <form @submit.prevent="login">
    <h4 class="text-center pt-2">Login</h4>
  <!-- Email input -->
  <div class="form-outline mb-4">
    <input type="email" id="form2Example1" class="form-control" v-model="user.email" />
    <label class="form-label" for="form2Example1">Email address</label>
  </div>

  <!-- Password input -->
  <div class="form-outline mb-4">
    <input type="password" id="form2Example2" class="form-control" v-model="user.password" />
    <label class="form-label" for="form2Example2">Password</label>
  </div>


  <!-- Submit button -->
  <button type="submit" class="btn btn-primary btn-block mb-4">Login</button>

  <!-- Register buttons -->
  <div class="text-center">
    <p>Not a member? <a href="/register">Register</a></p>
  </div>
</form>
</div>


</template>

<script>
import { useAuthStore } from "../stores/auth";
import { ref } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const user = ref({ email: "", pasword: "" });
    const authStore = useAuthStore();
    const router = useRouter();

    async function login() {
      await fetch("http://127.0.0.1:8000/api/login", {
        method: "post",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(user.value),
      })
        .then((response) => response.json())
        .then((data) => {
          if (data.status === "success") {
            authStore.saveAuth(data.user, data.token);
            router.push("/");
          } else {
            alert(data.message);
          }
        });
    }
    return {
      user,
      login,
    };
  },
};
</script>

<style></style>
