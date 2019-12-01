<template>
  <div class="container">
    <div class="bg-light mt-5 mb-5" style="padding:20px;">
      <h2 class="display-3">{{topic.title}} </h2>
      <hr>
      <p class="text-muted">{{topic.created_at}} by {{topic.user.name}} to create title</p>
      <div v-for="(content, index) in topic.posts" :key="index" class="ml-5 content">
        <p>{{content.body}}</p>
        <p class="text-muted">{{content.created_at}} by {{content.user.name}}</p>

        <div v-if="authenticated" class="mb-5">
          <div v-if="user.id === content.user.id">
            <nuxt-link
              :to="{name : 'topics-posts-edit-id-body' , params : {id : $route.params.id , body : content.id}}">
              <button class="btn btn-outline-success fa fa-edit pull-right borderE"></button>
            </nuxt-link>

            <button @click="deletePost(content.id)"
                    class="btn btn-outline-danger fas fa-trash-alt pull-right borderE"></button>


          </div>
        </div>


      </div>
    </div>

    <div class="mt-5 ml-5" v-if="authenticated">
      <form @submit.prevent="create">
        <div class="form-group">
          <h4>Add new comment</h4>
          <textarea v-model="body" class="form-control" rows="5"></textarea>
          <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>
        </div>

        <button type="submit" class="btn btn-outline-primary">Add a new post</button>

      </form>
    </div>
    <br>
    <br>

  </div>
</template>

<script>
  export default {
    name: "index",
    created() {
      this.getTopics
    },
    data() {
      return {
        topic: '',
        body: ''
      }
    },

    async asyncData({$axios, params}) {
      const {data} = await $axios.$get(`/topics/${params.id}`);
      return {
        topic: data
      }
    },
    methods: {
      async create() {
        this.$axios.$post(`/topics/${this.$route.params.id}/posts/`, {
          body: this.body
        });
        location.reload()
      },

      async deletePost(id) {
        const delMas = confirm("Are you sure to delete !");
        if (delMas === true) {
          await this.$axios.$delete(`/topics/${this.$route.params.id}/posts/${id}`);
          // this.$router.push('/')
          location.reload()
        }
      }
    }

  }
</script>

<style scoped>
  .borderE {
    border: none;
  }
</style>
