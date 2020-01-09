<template>
  <div id="app">
    <app-header></app-header>
    <app-teams v-show="!selected" @toggled="isSelected"></app-teams>
    <app-teaminfo v-show="myteam" v-bind:teamId='teamId'></app-teaminfo>
    <app-playerinfo v-show="selected" v-bind:teamId='teamId'></app-playerinfo>
    <button @click="isSelected">Back</button>

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
      selected: false,
      teamId: 0,
    };
  },
  methods: {
    isSelected(id) {
      this.teamId = id;
      this.selected = !this.selected;
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
