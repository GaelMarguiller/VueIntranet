<template>
    <div id="home-view">
        <h1>{{ welcomeMsg }}</h1>
        <h3>{{ description }}</h3>
        <hr>
        <br>
        <div class="title">Avez vous dit bonjour aujourd'hui à ...</div>
        <br>
        <div class="col s12 m8 offset-m2">
            <user-card :user="user" @remove="removeUser"></user-card>
            <a @click="randomUser" class="waves-effect waves-light btn"><i class="material-icons left">autorenew</i>Dire bonjour à quequ'un d'autre !</a>
        </div>
    </div>
</template>

<script>
    import users from '../data/users.json';
    import UserCard from "../data/components/user-card.vue";
    import * as axios from "mongodb";

    export default {
        name: 'home-view',
        components: {UserCard},
        data () {
            return {
                welcomeMsg: 'Bienvenue dans l\'intranet',
                description: 'La plate-forme social de l\'entreprise',
                user: users[0],
            }
        },
        created(){
            axios.get('http://localhost:8080/list');
            then(res => res.data);
            then(users => {
                console.log('les users du serveur sont,',users);
                this.users = users;

                this.randomUser()
            })
        },

        methods:{
            randomUser: function () {
                this.user = users[Math.floor(Math.random() * (users.length - 0 + 0)) + 0]
            },
            removeUser: function (user) {
                users.splice(user)
            }
        }
    }
</script>
