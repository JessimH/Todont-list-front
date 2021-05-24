<template>
  <div>
    <h1>Profil</h1>

    <div v-if="user.data">
      <p>Name: {{user.data.name}}</p>
      <p>Email: {{user.data.email}}</p>
    </div>
    <div v-else>Not logged.</div>
  </div>
</template>

<script>
import { mapGetters } from "vuex"

export default {
    name: "Me",
    data() {
        return {};
    },
    computed: {
        ...mapGetters({'user': 'auth/user'})
    }
}
</script>
