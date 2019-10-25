<template id="login-page">
  <div class="bg-gray-200 w-full h-screen md:px-12 md:py-12 sm:px-6 sm:py-6">
    <div class="w-full max-w-xs">
      <!-- TODO: Add Flash message -->
      <div v-if="showFlash">Showing some info</div>
      <div class="rounded bg-indigo-500 pt-1">
      </div>
      <div class="bg-white">
        <div class="pt-4 h-32 w-32 mx-auto">
          <img src="../assets/logo/logo.svg">
        </div>
        <form class="bg-white shadow-xl pt-6 px-8 pb-8 mb-4">
          <div class="pt-1 mb-1"></div>
          <div class="mb-4">
            <label
              class="block text-gray-700 text-sm font-bold mb-2"
              for="email"
            >
              Email
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="email"
              v-model="email"
              type="text"
              placeholder="email"
            >
          </div>
          <div class="mb-6">
            <label
              class="block text-gray-700 text-sm font-bold mb-2"
              for="password"
            >
              Password
            </label>
            <input
              class="shadow appearance-none border border-red-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password"
              v-model="password"
              type="password"
              placeholder="******************"
            >
            <p class="text-red-500 text-xs italic">Please choose a password.</p>
          </div>
          <div class="flex items-center justify-between">
            <button
              class="bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              @click="sendLogin"
            >
              Sign In
            </button>
            <a
              class="inline-block align-baseline font-bold text-sm text-indigo-500 hover:text-indigo-600"
              href="#"
            >
              Forgot Password?
            </a>
          </div>
        </form>
      </div>
      <p class="text-black">
        {{ errorMessage }}
      </p>
      <p class="text-center text-gray-500 text-xs">
        &copy;2019, <span class="text-indigo-500 font-semibold">My Company Corp.</span> All rights reserved.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  template: "#login-page",
  data() {
    return {
      email: "",
      password: "",
      errorMessage: "",
      showFlash: false
    };
  },
  methods: {
    sendLogin: function() {
      const data = { email: this.email, password: this.password };
      fetch("/api/login", {
        method: "POST",
        body: JSON.stringify(data),
        headers: {
          "Content-Type": "application/json"
        }
      })
        .then(resp => resp.json())
        //.then(j => JSON.stringify(j))
        .then(j => {
          if (j.status === "OK") {
            window.location.replace("/");
          } else {
            this.errorMessage = "Invalid input";
          }
        })
        .catch(e => console.error("e :", e)); /* eslint-disable-line */
    }
  }
};
</script>

<style>
@import url("https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"); /* TODO: Don't use the CDN */

.bg-logo {
  background-image: url("../assets/logo/logo.svg");
}
</style>