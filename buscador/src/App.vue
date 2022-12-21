<template>
  <div id="app">
    <Navbar/>
    <div class="container">
      <div class="card card-body">
        <h1>Procurar Usuários e Repositórios No GitHub </h1>
        <p class="lead">
          Digite um nome para pesquisar usuários 
        </p>
        <input @keyup= "getUser" id="search" type="text" class="form-control" required/>
      </div>
      <div class="row mt-3" v-if="user.length !==0">
        <div class="col-md-4">
          <Profile :user="user"/>
        </div>
        <div class="colmd-8">
          <Repo v-for="repo in repos" :key="repo" :repo="repo"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Repo from "./components/Repo.vue";
import Profile from "./components/Profile.vue";

import axios from 'axios';


export default {
  name: 'app',
  data(){
      return{
        github: {
    url: "https://api.github.com/users",
    client_id:"a7a7f86e98a307e7eb9a",
    client_secret: " d14b8454c28edc209ab2d0bc62c725efb138af45 ",
    count: 7,
    sort: "created: asc"
      },
      user:[],
      repos:[]
      };
  },
  components:{
    Navbar,
    Profile,
    Repo
  },
  methods:{
    getUser(e){
      const user= e.target.value;
      const{url,client_id,client_secret,count,sort } = this.github;

      axios.get(
        `${url}/${user}?client_id=${client_id}&client_secret=${client_secret}`
        ).then(({data}) => this.user =data);


        axios.get(`${url}/${user}/repos?per_page=${count}&sort=${sort}$client_id=${client_id}&client_secret=${client_secret}`).then(({data}) => this.repos = data)
    }
  }
 
};
</script>

