<template>
  <div>
    {{ teamInfo }}
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  props: ['teamId'],

  data() {
    return {
      teamInfo: null,
    };
  },
  mounted() {
    axios({
      method: 'GET',
      // eslint-disable-next-line prefer-template
      url: 'https://free-nba.p.rapidapi.com/teams/' + this.teamId,
      headers: {
        'content-type': 'application/octet-stream',
        'x-rapidapi-host': 'free-nba.p.rapidapi.com',
        'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
      },
      params: {
        page: '0',
      },
    }).then((response) => {
      this.teamInfo = response.data;
    });
  },
};
</script>
