<template>
  <div class="container">
    <div v-for="team in teamInfo" v-bind:key="team.id">
      <div class="py-5 text-center">
        <img
          :src="'../images/' + teamId+ '.png'"
          width="150px"
          height="150px"
          padding
        />
        <h2>{{ team.fullName }}</h2>
        <p class="lead">
          Below is an example form built entirely with Bootstrap's form
          controls. Each required form group has a validation state that can be
          triggered by attempting to submit the form without completing it.
        </p>
      </div>

      <div class="row">
        <div class="col-md-4 order-md-2 mb-4">
          <h4>Team Info</h4>
          <p class="d-flex justify-content-between align-items-center mb-3">
            <b>TEAM DIVISION: </b> {{ team.leagues.standard.divName }}
          </p>
          <p class="d-flex justify-content-between align-items-center mb-3">
            <b>TEAM CONFERENCE:</b> {{ team.leagues.standard.confName }}
          </p>
          <p class="d-flex justify-content-between align-items-center mb-3">
            <b>TEAM CITY:</b> {{ team.city }}
          </p>
        </div>
        <div class="col-md-8 order-md-1">
          <h4>2019 - 2020 Roster</h4>
          <ul v-for="player in players" v-bind:key="player.id">
            <li v-if="player.leagues.standard != null && player.leagues.standard.active == 1">
              {{ player.firstName }} {{ player.lastName }} {{ player.leagues.standard }}</li>
          </ul>
        </div>
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
      players: null,
    };
  },
  methods: {
    teamCall() {
      axios({
        method: 'GET',
        // eslint-disable-next-line prefer-template
        url: 'https://api-nba-v1.p.rapidapi.com/teams/teamId/' + this.teamId,
        headers: {
          'content-type': 'application/octet-stream',
          'x-rapidapi-host': 'api-nba-v1.p.rapidapi.com',
          'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
        },
        params: {
          page: '0',
        },
      }).then((response) => {
        this.teamInfo = response.data.api.teams;
      });
    },
    playerCall() {
      axios({
        method: 'GET',
        // eslint-disable-next-line prefer-template
        url: 'https://api-nba-v1.p.rapidapi.com/players/teamId/' + this.teamId,
        headers: {
          'content-type': 'application/octet-stream',
          'x-rapidapi-host': 'api-nba-v1.p.rapidapi.com',
          'x-rapidapi-key': 'gfetYKeN6VyxYZCQbYCF4TLt88QQnSoc',
        },
        params: {
          page: '0',
        },
      }).then((response) => {
        this.players = response.data.api.players;
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
  computed: {
    filteredPlayers() {
      const vm = this;
      const league = vm.players.leagues.standard;
      if (league != null) {
        return vm.people;
      }
      // eslint-disable-next-line func-names
      return vm.people.filter(person => person.category === league);
    },
  },
};
</script>
<style scoped>
.player {
  padding-right: 10px;
}
</style>
