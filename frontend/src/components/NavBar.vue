<template>

<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <!-- Container wrapper -->
  <div class="container-fluid">
    <!-- Toggle button -->
    <button
      class="navbar-toggler"
      type="button"
      data-mdb-toggle="collapse"
      data-mdb-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <i class="fas fa-bars"></i>
    </button>

    <!-- Collapsible wrapper -->
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <!-- Navbar brand -->
      <router-link class="navbar-brand mt-2 mt-lg-0" to="/">
        Midterm
      </router-link>
    </div>
    <!-- Collapsible wrapper -->

    <!-- Right elements -->
    <div class="d-flex align-items-center " v-if="token != ''">
      <!-- Avatar -->
      <div class="dropdown">
        <a
          class="dropdown-toggle d-flex align-items-center hidden-arrow"
          href="#"
          id="navbarDropdownMenuAvatar"
          role="button"
          data-mdb-toggle="dropdown"
          aria-expanded="false"
        >
          <img
            src="/avatar.png"
            class="rounded-circle"
            height="25"
            alt="Black and White Portrait of a Man"
            loading="lazy"
          />
        </a>
        <ul
          class="dropdown-menu dropdown-menu-end"
          aria-labelledby="navbarDropdownMenuAvatar"
        > 
          <li>
            <router-link to="/" class="dropdown-item">Home</router-link>
          </li>
          <li>
            <router-link to="/shouts" class="dropdown-item">Shouts</router-link>
          </li>
          <li>
            <router-link  to="/profile" class="dropdown-item">Profile</router-link>
          </li>
          <li>
            <a @click="logout" class="dropdown-item">Logout</a>
          </li>
        </ul>
      </div>
    </div>
    <!-- Right elements -->
  </div>
  <!-- Container wrapper -->
</nav>
<!-- Navbar -->

</template>

<script>
import { useAuthStore } from "../stores/auth";
import { useRouter } from "vue-router";
import { storeToRefs } from "pinia";
export default {
  setup() {
    const authStore = useAuthStore();
    const router = useRouter();

    const { token } = storeToRefs(useAuthStore());

    async function logout() {
      await fetch("http://localhost:8000/api/logout", {
        method: "post",
        headers: {
          Accept: "application/json",
          Authorization: "Bearer " + authStore.token,
        },
      })
        .then((response) => response.json())
        .then((data) => {
          if (data.status === "success") {
            authStore.destroy();
            router.push("/login");
          }
        });
    }

    return {
      logout,
      token,
    };
  },
};
</script>

<style scoped>
.hover-links:hover {
  color: blue;
}

.right-nav {
  width: 30%;
  display: flex;
  align-items: center;
  justify-content: center;
  align-content: center;
}
.right-nav ul {
  margin: 0;
}

.right-nav li {
  list-style: none;
}
.c-link {
  color: black;
}

.c-link:hover {
  color: blue;
}
</style>
