<template>
  <div id="nav">
    <router-link to="/">Accueil </router-link>
    
    <div v-if="!user.token">
      <router-link to="/register">Inscription</router-link>
      <router-link to="/login">Connexion</router-link>
    </div>
    
    <div v-if="user.token">
      <router-link to="/tasks">Tâches</router-link>
      <router-link to="/me">Profil</router-link>
      <a href="/home" @click.prevent="logout">Déconnexion</a>
    </div>
    
  </div>
  <router-view/>
</template>

<script>

    import { mapActions } from "vuex"
    import { mapGetters } from "vuex"


    export default {
      data() {
            return {};
        },
        computed: {
            ...mapGetters({'user': 'auth/user'})
        },
        methods: {
            ...mapActions({'logout': 'auth/logout'})
        }
    }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color: black;
}

#nav {
  width: 100vw;
  padding: 30px;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

#nav a {
  font-weight: bold;
  margin-right: 15px;
  color: black;
}

#nav a.router-link-exact-active {
  color: #149e2b;
}
</style>
