<template>
  <div>
    <h1>Task: </h1>
    <form v-if="user.token">
        <p v-if="msg.success" style="color: green">{{msg.success}}</p>
                <div class="form-group">
                    <label for="body">Body:</label><br>
                    <textarea type="text" name="body" class="form-control" id="exampleFormControlInput1" v-model="form.body"></textarea><br>
                </div>
                <button type="button" class="btn btn-primary" v-if="form.body.length !=0" @click.prevent="create(form)">Ajouter un tâche</button>
    </form>
    <div v-else>Not logged.</div>
  </div>
</template>

<script>

    import { mapActions } from "vuex"
    import { mapGetters } from "vuex"
    export default {
        name: "Create",
        data() {
            return {
                form: {
                    body: ''
                }
            };
        },
        computed: {
            ...mapGetters({'user': 'auth/user'}),
            ...mapGetters({'msg': 'auth/msg'})
        },
        methods: {
            ...mapActions({'createTask': 'auth/createTask'}),
            create(form){
                this.createTask(form)
                this.$router.push('/tasks');
            }
        },
        mounted(){
            this.msg.success = ''
        }
    }
</script>