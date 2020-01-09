<template>
  <div id="app">
    <app-header></app-header>
    <app-teams v-show="teams" @toggled="teamSelected"></app-teams>
    <app-teaminfo v-show="teamSelect" v-bind:teamId='teamId' @playerPick="PlayerPicked">
    </app-teaminfo>
    <app-playerinfo v-show="playerSelect" v-bind:teamId='teamId'></app-playerinfo>

    <button v-show="teamSelect" @click="teamSelected">Back to Teams</button>
    <button v-show="playerSelect" @click="playerSelected">Back to Team</button>

  </div>
</template>

<script>
import teams from './components/teams.vue';
import teaminfo from './components/teaminfo.vue';
import header from './components/header.vue';
import playerinfo from './components/playerinfo.vue';

export default {
  name: 'app',
  data() {
    return {
      teams: true,
      teamSelect: false,
      playerSelect: false,
      teamId: 0,
      playerName: '',
    };
  },
  methods: {
    playerSelected() {
      this.teamSelect = !this.teamSelect;
      this.playerSelect = !this.playerSelect;
      this.$forceUpdate();
    },
    teamSelected(id) {
      this.teamId = id;
      this.teams = !this.teams;
      this.teamSelect = !this.teamSelect;
      this.$forceUpdate();
    },
    PlayerPicked(name) {
      this.playerName = name;
      this.teamSelect = !this.teamSelect;
      this.playerSelect = !this.playerSelect;
      this.$forceUpdate();
    },
  },
  components: {
    appTeams: teams,
    appTeaminfo: teaminfo,
    appHeader: header,
    appPlayerinfo: playerinfo,
  },
};
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
ul {
  list-style-type: none;
}
/* Move down content because we have a fixed navbar that is 3.5rem tall */
body {
  padding-top: 3.5rem;
}
</style>
