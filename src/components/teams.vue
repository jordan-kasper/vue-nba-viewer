<template>
  <div>
    <ul>
      <li v-for="post of posts.data" v-bind:key="post.id">
        <p @click="teamSelected(post.id)">{{ post.full_name }}</p>
      </li>
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
