<template>
  <div id="app">
    <Navbar/>
    <div class="container">
      <div class="card card-body">
        <h1>Procurar Usuários e Repositórios No GitHub </h1>
        <p class="lead">
          Digite um nome para pesquisar usuários 
        </p>
        <input id="search" type="text" class="form-control" required/>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
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
    Navbar
  },
  methods:{
    getUser(e){
      const user= e.target.value;
      const{url,client_id,client_secret } = this.github;

      axios.get(
        `${url}/${user}?client_id=${client_id}&client_secret=${client_secret}`
        ).this(({data}) => this.user =data);
    }
  }
 
};
</script>

