<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
    <app-teams v-show="!selected" @toggled="isSelected"></app-teams>
    <app-teaminfo v-show="selected" v-bind:teamId='teamId'></app-teaminfo>
    <button @click="isSelected">Back</button>
  </div>
</template>

<script>
import teams from './components/teams.vue';
import teaminfo from './components/teaminfo.vue';

export default {
  name: 'app',
  data() {
    return {
      selected: false,
      teamId: 1,
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
</style>
