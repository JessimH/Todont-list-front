<template>
  <div>
    <h1>Task: </h1>
    <form v-if="user.token">
        <p v-if="msg.success">{{msg.success}}</p>
        <div class="form-group">
            <label for="body">Body:</label>
            <textarea type="text" name="body" class="form-control" v-model="task.body"></textarea>
        </div>
        <button type="button" class="btn btn-primary mr-2" v-if="task.body.length !=0" @click.prevent="updateTask(task)">Modifier</button>
        <button type="button" class="btn btn-danger ml-2" @click.prevent="deleteTask(task)" style="margin-right: 2%">Supprimer</button>
    </form>
    <div v-else>Not logged.</div>
  </div>
</template>

<script>
import { mapActions } from "vuex"
import { mapGetters } from "vuex"
export default {
    name: "Task",
    data() {
        return {
        };
    },
    computed: {
        ...mapGetters({'user': 'auth/user'}),
        ...mapGetters({'msg': 'auth/msg'}),
            ...mapGetters({'task': 'auth/task'})
    },
    mounted(){
        this.task_user(this.$route.params.id)
        this.msg.success = ''
    },
    methods: {
        ...mapActions({'task_user': 'auth/task_user'}),
        ...mapActions({'updateTask': 'auth/updateTask'}),
        ...mapActions({'deleteTask': 'auth/deleteTask'}),
        delTask(task){
            this.deleteTask(task)
            this.$router.push('/tasks');
        },
        upTask(task){
            this.updateTask(task)
            this.$router.push('/tasks');
        }
    }
}
</script>