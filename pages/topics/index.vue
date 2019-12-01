<template>
  <div class="container">

    <div v-for="(topic , index) in topics" :key="index" class="bg-light mt-5 mb-5" style="padding: 20px">
      <h2>
        <nuxt-link :to="{name : 'topics-id' , params : {id : topic.id}}">{{topic.title}}</nuxt-link>
      </h2>

      <p class="text-muted">{{topic.created_at}} by {{topic.user.name}} </p>

      <div v-for="(content , index) in topic.posts" :key="index" class="ml-5 content">
        {{content.body}}
        <p class="text-muted">{{content.created_at}} by {{content.user.name}} </p>
      </div>

      <div v-if="authenticated">
        <div v-if="user.id === topic.user.id">
          <nuxt-link :to="{name : 'topics-edit-id' , params : {id : topic.id}}">
            <button class="btn btn-outline-success fa fa-edit fa-2x pull-right"></button>
          </nuxt-link>

          <button @click="deleteTopic(topic.id)"
                  class="btn btn-outline-danger fas fa-trash-alt fa-2x pull-right"></button>

        </div>
      </div>

    </div>
    <nav>
      <ul class="pagination justify-content-center">
        <li v-bind:class="[{disabled: !links.prev}]" class="page-item"><a class="page-link" href="#"
                                                                          @click="getTopics(links.prev)">Previous</a>
        </li>

        <li class="page-item disabled"><a class="page-link text-dark" href="#">Page {{ meta.current_page }} of {{
          meta.last_page }}</a></li>

        <li v-bind:class="[{disabled: !links.next}]" class="page-item"><a class="page-link" href="#"
                                                                          @click="getTopics(links.next)">Next</a></li>
      </ul>
    </nav>
  </div>
</template>

<script>
  export default {
    name: "index",
    created() {
      this.getTopics()
    },
    data() {
      return {
        topics: '',
        links: {},
        meta: {},
      }
    },
    methods: {
      getTopics(page_url) {
        page_url = page_url || '/topics';
        this.$axios.get(page_url)
          .then(res => {
            this.topics = res.data.data;
            this.links = res.data.links;
            this.meta = res.data.meta;
          })
      },

      async deleteTopic(id) {
        const delMas = confirm("Are you sure to delete !");
        if (delMas === true) {
          await this.$axios.$delete(`/topics/${id}`);
          location.reload()
        }
      }
    }
  }
</script>

<style scoped>

</style>
