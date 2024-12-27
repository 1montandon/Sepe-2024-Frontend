<script setup>
import { ref, computed } from 'vue';
import { useAuthStore } from '@/stores/auth'; 
import { useJogoStore } from '@/stores';
import TableHeadersEye from 'vue-material-design-icons/TableHeadersEye.vue';
import Soccer from 'vue-material-design-icons/Soccer.vue';

const authStore = useAuthStore();
const jogoStore = useJogoStore();

const isLogged = computed(() => authStore.isLogged);
const user = computed(() => authStore.user);

</script>

<template>
<header>
  <div class="logo">
      <router-link to="/"> <img src="https://i.ibb.co/9VfWVgh/COPAO-1.png" alt="logo"></router-link>
    </div>
    <nav class="nav-links">
      <router-link to="/tabela" 
      
      :class="{'nav-item nav-item-select': $route.path === '/tabela','nav-item': $route.path !== '/tabela'}">

      <TableHeadersEye :class="{'icon icon-select': $route.path === '/tabela','icon': $route.path !== '/tabela'}"></TableHeadersEye> 
      Classificação

      </router-link>

      <router-link to="/chaveamento"       
      
        :class="{'nav-item nav-item-select': $route.path === '/chaveamento','nav-item': $route.path !== '/chaveamento'}">
        
        <img src="https://i.ibb.co/MDkmH5j/Chavemante-Vector.png" alt="" class="icon"> Chaveamento
      
      </router-link>
          
      <router-link to="/jogos" :class="{'nav-item nav-item-select': $route.path === '/jogos','nav-item': $route.path !== '/jogos'}">
        
        <Soccer :class="{'icon icon-select': $route.path === '/jogos','icon': $route.path !== '/jogos'}"></Soccer> 
      Jogos</router-link>
    </nav>

    <nav v-if="authStore.isAdmin" class="nav-admin">
        <router-link to="/crudjogo" :class="{'nav-item nav-item-select': $route.path === '/crudjogo','nav-item': $route.path !== '/crudjogo'}">
          Crud Jogo
        </router-link>

        <router-link to="/crudtime" :class="{'nav-item nav-item-select': $route.path === '/crudtime','nav-item': $route.path !== '/crudtime'}">
          Crud Time
        </router-link>

        <router-link to="/crudjogador" :class="{'nav-item nav-item-select': $route.path === '/crudjogador','nav-item': $route.path !== '/crudjogador'}">
          Crud Jogador
        </router-link>

        <div class="nav-item" @click="jogoStore.gerarSemis()">
          Gerar Semis
        </div>

        <div class="nav-item" @click="jogoStore.gerarFinal()">
          Gerar Final
        </div>

      </nav>
    
    <router-link class="perfilBorder" v-if="isLogged" to="/perfil">
      <img :src=" user.foto ? user.foto : 'https://i.ibb.co/kmyjjy3/Default-pfp-svg.png'" alt="">
       </router-link>

    <router-link v-else to="/login" class="loginBorder">
      Sing In
    </router-link>
  </header>  
  </template>

<style scoped>
.perfilBorder{
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #313131;
  border-radius: 50%;
  width: 3vw;
  height: 3vw;
  margin-left: auto;
  margin-right: 2%;
  
  img{
    border-radius: 50%;
    width: 80%;
  }
}
.loginBorder{
  all:unset;
  padding: 0.4% 1% 0.4% 1%;
  border-radius: 0.9rem;
  background-color: var(--white);
  margin-left: auto;
  font-size: 1rem;
  color: var(--black);
  cursor: pointer;
  font-weight: 700;
}
header {
  display: flex;
  background-color: var(--mid-grey);
  height: 110px;
  width: 100%;
  padding: 1.25rem;
  align-items: center;
}

.logo img {
  width: 200px;
}
.icon{
  color: #757575;
  transition: all .2s; 
  display: flex;

}

.nav-links {
  display: flex;
  gap: 2.5rem;
  margin-left: 40px;

}
.nav-admin{
  display: flex;
  gap: 2.5rem;
  margin-left: auto;

}

.nav-item {
  color: #757575;
  text-decoration: none;
  font-size: 1.125rem;
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.3rem;
  cursor: pointer;
  transition: all .1s;
}
.nav-item-select{
  color: white;
}
.icon-select{
  color: white;
  transition: all .2s;
}
.nav-item-select::after {
  content: '';
  position: absolute;
  bottom: -40px;
  left: 0;
  width: 100%;
  height: 0.5vh;
  background-color: white;
  border-radius: 10px 10px 0px 0px;
  transition: all .2s;
}
</style>
