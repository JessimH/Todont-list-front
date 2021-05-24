<template>
  <div>
    <router-link to="/create"><button type="button" class="btn btn-primary mb-4">Créer une tache</button></router-link>
    <h1>Taches a ne pas faire: </h1>
    <div v-if="user.token">
        <br>
     <div v-for="task in tasks" :key="task.id" class="container">
         <br>
         <div class="task">
             <br>
             <router-link :to="{ path: '/tasks/'+ task.id}">
                <p>{{ task.body }}</p>
            </router-link>
         </div>
         <br><br>
    </div>
    </div>
    <div v-else>Not logged.</div>
  </div>
</template>

<script>

    import { mapActions } from "vuex"
    import { mapGetters } from "vuex"
    export default {
        name: "Tasks",
        data() {
            return {};
        },
        computed: {
            ...mapGetters({'user': 'auth/user'}),
             ...mapGetters({'tasks': 'auth/tasks'})
        },
        methods: {
            ...mapActions({'tasks_user': 'auth/tasks_user'})

        },
        mounted(){
                this.tasks_user()
                console.log("taches" + this.tasks)            
        }
    }
</script>
<style scoped>
.container{
    display: flex;
    justify-content: center;
}
    .task{
        box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
        border-radius: 7px;
        margin: 5px;
        width: 50%;
        font-weight: 600;
    }
    .task a{
        color: #149e2b;
    }
</style>