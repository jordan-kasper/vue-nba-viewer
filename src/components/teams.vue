<template>
  <div class="container">
    <ul>
      <div class="row">
      <li v-for="post of posts.data" v-bind:key="post.id">
        <div class="logo">
          <img :src="'../images/' + post.id + '.png'"
          @click="teamSelected(post.id)" width="150px" height="150px" padding>
        </div>
      </li>
      </div>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  data() {
    return {
      posts: [],
      selected: false,
    };
  },
  mounted() {
    axios({
      method: 'GET',
      url: 'https://free-nba.p.rapidapi.com/teams',
      headers: {
        'content-type': 'application/octet-stream',
        'x-rapidapi-host': 'free-nba.p.rapidapi.com',
        'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
      },
      params: {
        page: '0',
      },
    }).then((response) => {
      this.posts = response.data;
    });
  },
  methods: {
    teamSelected(id) {
      this.$emit('toggled', (id));
    },
  },
};
</script>

<style scoped>

</style>
