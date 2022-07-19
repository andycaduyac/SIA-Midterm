<template>
<div class="container">
  <section class="vh-80">
  <div class="container py-5 h-80">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col col-md-9 col-lg-7 col-xl-5">
        <div class="card bg-dark" style="border-radius: 15px;">
          <div class="card-body p-4">
            <div class="d-flex">
              <div class="flex-shrink-0">
                <img src="/avatar.png"
                  alt="Generic placeholder image" class="img-fluid"
                  style="width: 180px; border-radius: 10px;">
              </div>
              <div class="flex-grow-1 ms-3" style="color: #e2e2e2;">
                <h5 class="mb-1">{{user.fname}} {{user.lname}}</h5>
                <p class="mb-2 pb-1" style="color: #e2e2e2;">{{user.course}} {{user.year}}</p>
                <div class="d-flex justify-content-start rounded-3 p-2 mb-2"
                  style="background-color: grey;">
                  <div>
                    <p class="small mb-1">Mobile</p>
                    <p class="mb-0">{{user.mobile}}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
</div>

</template>

<script>
import { useAuthStore } from "../stores/auth";
import { useRouter } from "vue-router";

export default {
  setup() {
    const { user, token } = useAuthStore();
    const router = useRouter();

    if (token == "") {
      router.replace("/login");
    }

    return {
      user,
      token,
    };
  },
};
</script>

<style></style>
