<template> 
  <div class="container"><section class="vh-100 gradient-custom">
    <div class="container py-5 h-50">
      <div class="row justify-content-center align-items-center h-100">
        <div class="col-12 col-lg-9 col-xl-7">
          <div class="card shadow-2-strong card-registration" style="border-radius: 15px;">
            <div class="card-body p-4 p-md-5">
                <h3 class="mb-4 pb-2 pb-md-0 mb-md-5">Registration Form</h3>
                <form @submit.prevent="handleSubmit">

                  <div class="row">
                    <div class="col-md-6 mb-4">

                      <div class="form-outline">
                        <input type="text" id="firstName" class="form-control form-control-lg" v-model="user.fname" />
                        <label class="form-label" for="firstName">First Name</label>
                      </div>

                    </div>
                    <div class="col-md-6 mb-4">

                      <div class="form-outline">
                        <input type="text" id="lastName" class="form-control form-control-lg" v-model="user.lname"/>
                        <label class="form-label" for="lastName">Last Name</label>
                      </div>

                    </div>
                  </div>

                  <div class="row">
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="text" id="course" class="form-control form-control-lg" v-model="user.course" />
                        <label class="form-label" for="course">Course</label>
                      </div>

                    </div>
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="text" id="year" class="form-control form-control-lg" v-model="user.year" />
                        <label class="form-label" for="year">Year</label>
                      </div>

                    </div>
                    
                  </div>
                  <div class="row">
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="tel" id="mobile" class="form-control form-control-lg" v-model="user.mobile" />
                        <label class="form-label" for="mobile">Mobile</label>
                      </div>

                    </div>
                    
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="text" id="address" class="form-control form-control-lg" v-model="user.address" />
                        <label class="form-label" for="address">Address</label>
                      </div>

                    </div>
                  </div>

                  
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="email" id="emailAddress" class="form-control form-control-lg" v-model="user.email" />
                        <label class="form-label" for="emailAddress">Email</label>
                      </div>

                    </div>
                    <div class="col-md-6 mb-4 pb-2">

                      <div class="form-outline">
                        <input type="password" id="phoneNumber" class="form-control form-control-lg" v-model="user.password" />
                        <label class="form-label" for="phoneNumber">Password</label>
                      </div>

                    </div>

                  <div class="mt-4 pt-2">
                    <input class="btn btn-primary btn-lg" type="submit" value="Register" />
                  </div>

                </form>
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
import { ref } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const user = ref({
      lname: "",
      fname: "",
      course: "",
      year: "",
      mobile: "",
      address: "",
      email: "",
      password: "",
    });
    const authStore = useAuthStore();
    const router = useRouter();

    async function handleSubmit() {
      await fetch("http://localhost:8000/api/register", {
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
            console.log(data.user);
            console.log(data.token);
            router.push("/");
          }
        });
    }
    return {
      user,
      handleSubmit,
    };
  },
};
</script>

<style></style>
