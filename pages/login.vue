<template>
  <div class="container w-50 jumbotron vertical-center  align-content-center mt-5">
    <h2 class="font-weight-bold">Login</h2>
    <form @submit.prevent="submit" method="post">
      <div class="form-group">
        <label for="Email">Email address</label>
        <input v-model.trim="form.email" type="email" class="form-control" id="Email" aria-describedby="emailHelp"
               placeholder="Enter email">
        <small class="form-text text-danger" v-if="errors.email">{{errors.email[0]}}</small>
      </div>
      <div class="form-group">
        <label for="Password">Password</label>
        <input v-model.trim="form.password" type="password" class="form-control" id="Password" placeholder="Password">
        <small class="form-text text-danger" v-if="errors.password">{{errors.password[0]}}</small>

      </div>
      <!--    <div class="form-group form-check">-->
      <!--      <input v-model="rememberMe" type="checkbox" class="form-check-input" id="RememberMe">-->
      <!--      <label class="form-check-label" for="RememberMe">Remember me</label>-->
      <!--    </div>-->
      <button type="submit" class="btn btn-primary">Login</button>
      <button type="reset" class="btn btn-dark">Reset</button>
    </form>

    <p class="mt-4">Dont have account ?
      <nuxt-link v-bind:to="{name : 'register'}">Registration</nuxt-link>
    </p>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex'

  export default {
    name: "login",
    middleware: ["guest"],
    data() {
      return {
        form: {
          email: '',
          password: '',
        },
        rememberMe: false

      }
    }, methods: {
      async submit() {
        await this.$auth.loginWith("local", {
          data: this.form
        }).catch(error => {
        });
        // return this.$router.push('/')
        // return this.$axios.post('/remember-my' , this.rememberMe)
        //        .then(res => console.log(res))
        //        .catch(erorr => console.log(erorr))

      }
    }
  }
</script>

<style scoped>

</style>
