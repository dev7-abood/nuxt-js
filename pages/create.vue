<template>
  <div class="container w-75 jumbotron vertical-center mt-4">
    <h2 class="font-weight-bold text-uppercase">create a new topic</h2>


    <form @submit.prevent="create" method="post">
      <label for="title" class="font-weight-bold mt-4">Create a new topic title</label>

      <input id="title" v-model="form.title" class="form-control" type="text" placeholder="Topic title ...">
      <small class="form-text text-danger" v-if="errors.title">{{errors.title[0]}}</small>

      <label for="body" class="font-weight-bold mt-4">Create a new topic ...</label>

      <textarea v-model="form.body" class="form-control" id="body" rows="3"></textarea>
      <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>

      <button type="submit" class="btn btn-primary mt-4">submit</button>
      <button type="reset" class="btn btn-dark mt-4">cancel</button>
    </form>


  </div>
</template>

<script>
  export default {
    name: "dashboard",
    middleware: ['auth'],
    data() {
      return {
        form: {
          title: '',
          body: ''
        }
      }
    },
    methods: {
      async create() {
        await this.$axios.$post('/topics', this.form)
          .catch(error => console.log(error));
        return this.$router.push('/topics')
      }
    }
  }
</script>

<style scoped>
  .container {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);

  }
</style>
