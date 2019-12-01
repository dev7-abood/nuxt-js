<template>
  <div class="container  w-50 jumbotron vertical-center  align-content-center mt-5">
    <h2 class="font-weight-bold">Registration</h2>

    <form @submit.prevent="submit" method="post">
      <div class="form-group">
        <label for="name">Full name</label>
        <input v-model.trim="form.name" type="text" class="form-control" id="name" placeholder="Full name" autofocus>
        <small class="form-text text-danger" v-if="errors.name">{{errors.name[0]}}</small>

      </div>

      <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input v-model.trim="form.email" type="email" class="form-control" id="exampleInputEmail1"
               aria-describedby="emailHelp" placeholder="Enter email">
        <small class="form-text text-danger" v-if="errors.email">{{errors.email[0]}}</small>
      </div>

      <div class="form-group">
        <label for="Password">Password</label>
        <input v-model.trim="form.password" type="password" class="form-control" id="Password" placeholder="Password">
        <small class="form-text text-danger" v-if="errors.password">{{errors.password[0]}}</small>

      </div>

      <div class="form-group">
        <label for="ConfirmPassword">Confirm Password</label>
        <input v-model.trim="confirmPassword" type="password" class="form-control" id="ConfirmPassword"
               placeholder="Confirm Password">
      </div>

      <button type="submit" class="btn btn-primary">Register</button>
      <button type="reset" class="btn btn-dark">Reset</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: "register",
    middleware: ["guest"],

    data() {
      return {
        form: {
          name: '',
          email: '',
          password: ''
        },
        confirmPassword: ''
      }
    },
    methods: {
      submit() {
        this.$axios.post('/auth/register', this.form)
          .then(
            this.$auth.loginWith("local", {
                data: {
                  email: this.form.email,
                  password: this.form.password,
                }
              }
            )
          )
          .then(
            this.$router.push('/')
          )


        // redirect
      }
    }
  }
</script>

<style scoped>

</style>
