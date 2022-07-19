<template>
  <div class="container">
    <h4 class="text-center p-3">Shouts</h4>
      <table class="table table-hover">
    <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Shoutout</th>
        <th scope="col">Tags</th>
        <th scope="col">User ID</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="list in shouts" :key="list.id">
          <td>{{ list.id }}</td>
          <td>{{ list.shoutout }}</td>
          <td>{{ list.tags }}</td>
          <td>{{ list.user_id }}</td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
import { useAuthStore } from "../stores/auth";
import { useRouter } from "vue-router";
import { storeToRefs } from "pinia";
import { ref } from "vue";
export default {
  data() {
    return {
      shouts: [],
      token: "",
    };
  },
  methods: {
    getData() {
      const authStore = useAuthStore();
      const router = useRouter();

      const { token } = storeToRefs(useAuthStore());
      this.token = token;

      fetch("http://localhost:8000/api/shouts/", {
        method: "get",
        headers: {
          Accept: "application/json",
          Authorization: "Bearer " + authStore.token,
        },
      })
        .then((data) => data.json())
        .then((data) => (this.shouts = data))
        .catch((err) => console.log(err));
    },
  },

  mounted() {
    this.getData();
    const router = useRouter();

    console.log("mounted");
    if (this.token == "") {
      router.replace("/login");
    }
  },
};
</script>

<style></style>
