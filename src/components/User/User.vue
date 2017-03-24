<template lang="html">
<div>
  <p class="app-tagline">Utilisateur : {{maker.name}}</p>
  <ul>Projets :
    <li v-for="post in maker.maker_of">{{ post.name }} {{ post.id}}</li>
    <img :src="maker.image_url['30px']">

  </ul>

</div>
</template>

<script>
import axios from 'axios'
import _ from 'lodash'
import PostsListItem from '../PostsListItem/PostsListItem.vue'
export default {

  components: {
              'posts-list-item': PostsListItem
          },

  data() {
    return {
      maker: null,
    }
  },

  created() {

            this.getMaker(this.$route.params.makerId)
        },
        methods: {

            getMaker(makerId) {

                axios.get('/v1/users/' + makerId)
                    .then((response) => {
                        console.log(response.data.user)
                        this.maker = response.data.user
                    })
                    .catch(function (error) {
                        console.log(error)
                    })
            }
        }
}
</script>

<style lang="css">
</style>
