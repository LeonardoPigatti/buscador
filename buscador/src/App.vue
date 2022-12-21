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
      <div class="row" v-if="user.length !==0">
        <div class="col-md-4">
          <Profile :user="user"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
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
    Profile
  },
  methods:{
    getUser(e){
      const user= e.target.value;
      const{url,client_id,client_secret } = this.github;

      axios.get(
        `${url}/${user}?client_id=${client_id}&client_secret=${client_secret}`
        ).then(({data}) => this.user =data);
    }
  }
 
};
</script>

