<template>
  <div class="container">

         <div class="py-5 text-center">
        <img :src="'../images/' + teamInfo.id + '.png'" width="150px" height="150px" padding>
        <h2>{{teamInfo.full_name}}</h2>
        <p class="lead">Below is an example form built entirely with Bootstrap's form controls.
          Each required form group has a validation state that can be triggered by attempting
          to submit the form without completing it.</p>
      </div>

      <div class="row">
        <div class="col-md-4 order-md-2 mb-4">
          <h4>Team Info</h4>
          <p class="d-flex justify-content-between align-items-center mb-3">
            <b>TEAM DIVISION: </b> {{teamInfo.division}}
          </p>
          <p class="d-flex justify-content-between align-items-center mb-3">
            <b>TEAM CONFERENCE:</b> S{{teamInfo.conference}}
</p>
            <p class="d-flex justify-content-between align-items-center mb-3">
              <b>TEAM CITY:</b> {{teamInfo.city}}</p>
        </div>
        <div class="col-md-8 order-md-1">
          <h4>2019 - 2020 Roster</h4>
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
                  <img src="../images/user.png" width="150px" height="150px"
                  style="padding-right: 10px; padding-bottom: 10px">
        </div>
  </div>
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
      players: [],
    };
  },
  methods: {
    teamCall() {
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
    playerCall() {
      axios({
        method: 'GET',
        // eslint-disable-next-line prefer-template
        url: 'https://free-nba.p.rapidapi.com/players/',
        headers: {
          'content-type': 'application/octet-stream',
          'x-rapidapi-host': 'free-nba.p.rapidapi.com',
          'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
        },
        params: {
          page: '0',
        },
      }).then((response) => {
        this.players = response.data;
      });
    },
  },
  watch: {
    $props: {
      handler() {
        this.teamCall();
        this.playerCall();
      },
      deep: true,
      immediate: true,
    },
  },
};
</script>
<style scoped>
  .player{
    padding-right: 10px,
  }
</style>
