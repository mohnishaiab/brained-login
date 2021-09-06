<template>
  <div
    class="
      h-screen
      flex
      w-full
      bg-img
      vx-row
      no-gutter
      items-center
      justify-center
      relative
    "
  >
    <div class="vx-col sm:w-1/2 md:w-1/2 lg:w-3/4 xl:w-3/5 sm:m-0 absolute">
      <b-card no-body class="bg-secondary border-0 mb-0 p-0">
        <b-card-body class="flex p-0 fullpage-bgcolor">
          <div class="w-1/2 flex items-center justify-center">
            <img src="" alt="login" class="mx-auto" />
          </div>
          <div class="w-1/2 bg-white">
            <div class="p-4 login-tabs-container">
              <validation-observer
                v-slot="{ handleSubmit }"
                ref="formValidator"
              >
                <div class="mb-4">
                  <h4 class="mb-2 text-xl font-medium">Login</h4>
                  <p class="text-lg">
                    Welcome back, please login to your account.
                  </p>
                </div>
                <b-form role="form" @submit.prevent="handleSubmit(onSubmit)">
                  <b-form-input
                    alternative
                    class="mb-3"
                    name="Mobile"
                    :rules="{ required: true }"
                    prepend-icon="ni ni-email-83"
                    placeholder="Mobile"
                    v-model="mobile"
                  >
                  </b-form-input>

                  <b-form-input
                    alternative
                    class="mb-3"
                    name="Password"
                    :rules="{ required: true, min: 6 }"
                    prepend-icon="ni ni-lock-circle-open"
                    type="password"
                    placeholder="Password"
                    v-model="password"
                  >
                  </b-form-input>

                  <div class="flex flex-wrap justify-between my-2">
                    <router-link :to="{ name: 'forgot-password' }"
                      >Forgot Password?</router-link
                    >
                    <b-button
                      type="primary"
                      native-type="submit"
                      class="w-full mb-3"
                      >Login</b-button
                    >
                  </div>
                  <div class="cust-divider3"></div>
                  <div>
                    <p class="text-danger my-2 text-base">
                      Not yet registered ?
                    </p>
                    <b-button
                      type="primary"
                      outline
                      class="w-full mb-2"
                      @click="handleClick('register-with-password')"
                      >Register</b-button
                    >
                  </div>
                </b-form>
              </validation-observer>
            </div>
          </div>
        </b-card-body>
      </b-card>
    </div>
  </div>
</template>

<script>
import { BCard, BCardBody, BForm, BFormInput, BButton } from "bootstrap-vue";
import { ValidationObserver, extend } from "vee-validate";
import { required } from "vee-validate/dist/rules";

extend("required", {
  ...required,
  message: "This field is required",
});
import "tailwindcss/tailwind.css";

export default /*#__PURE__*/ {
  name: "BrainedLogin",
  components: {
    BCard,
    BCardBody,
    BForm,
    BFormInput,
    BButton,
    ValidationObserver,
  },
  data() {
    return {
      mobile: "",
      password: "",
      rememberMe: false,
    };
  },
  methods: {
    async onSubmit() {
      // this will be called only after form is valid. You can do api call here to login
      const payload = {
        mobile: this.mobile,
        password: this.password,
      };

      let loader = this.$loading.show({});
      try {
        await this.$store.dispatch("auth/loginWithPassword", payload);
        this.$router.push({ name: "channel" });
        loader.hide();
      } catch (error) {
        loader.hide();
      }
    },
    handleClick(name) {
      this.$router.push({ name: name });
    },
  },
};
</script>

<style>
.login-tabs-container {
  min-height: 505px;
}
.cust-divider3 {
  border-bottom: 3px solid #e9ecef;
}
.fullpage-bgcolor {
  background-color: #eff2f7;
}
.bor {
  border: 1px solid rgba(155, 154, 154, 0.623);
}
</style>
