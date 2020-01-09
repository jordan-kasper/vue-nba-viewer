<template>
  <div class="container">
        <ul>
      <div class="row">
      <li v-for="post of posts" v-bind:key="post.id">
        <div v-if="post.leagues.standard.confName == 'East' ||
        post.leagues.standard.confName == 'West'">
        <div v-if="post.logo !== ''">
          <img :src="post.logo"
          @click="teamSelected(post.teamId)" width="160px" height="160px"
          style="margin-right:11px; margin-left:11px; margin-top:50px; margin-bottom:20px">
          <p>{{post.shortName}}</p>
        </div>
        <div v-else>
          <img src="../assets/images/noimage.png"
          @click="teamSelected(post.teamId)" width="160px" height="160px"
          style="margin-right:11px; margin-left:11px; margin-top:50px; margin-bottom:20px">
          <p>{{post.shortName}}</p>
        </div>
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
