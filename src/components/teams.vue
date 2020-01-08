<template>
  <div class="container">
        <ul>
      <div class="row">
      <li v-for="post of posts" v-bind:key="post.id">
        <div v-if="post.leagues.standard.confName == 'East' ||
        post.leagues.standard.confName == 'West'">
          <img :src="'../images/' + post.teamId + '.png'"
          @click="teamSelected(post.teamId)" width="150px" height="150px" padding>
          <p>{{post.shortName}}</p>
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
      url: 'https://api-nba-v1.p.rapidapi.com/teams/league/standard',
      headers: {
        'content-type': 'application/octet-stream',
        'x-rapidapi-host': 'api-nba-v1.p.rapidapi.com',
        'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
      },
      params: {
        page: '0',
      },
    }).then((response) => {
      this.posts = response.data.api.teams;
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
