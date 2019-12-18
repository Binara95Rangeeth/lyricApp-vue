<template>
<div class="bg">
  <v-app>
    <div class="main">
      <div class="navbar">
      </div>
      
      <Search  
        v-on:myevent="updateSearchData($event)"/>
      
      <Lyric 
        v-if="this.isData"
        v-bind:searchData="searchData"/>
      
    </div>
      
  </v-app>
  </div>
</template>

<script>
import Search from './components/Search'
import Lyric from './components/Lyric'

export default {
  name: 'App',

  components: {
    Search,
    Lyric,
  },
  data(){
    return{
      searchData: {},
      isData : false,
    }
  },

  methods: {
    updateSearchData(data){
        this.searchData = data
        this.searchData == ""?this.isData = false:this.isData = true
      },
    
  }
};
</script>
<style scoped>
  .main{
    margin: 0;
    width: 100%;
    height: 100%;
    font-family: "Exo", sans-serif;
    color: #fff;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradientBG 15s ease infinite;
  }


  @keyframes gradientBG {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }


  .navbar{
    width: 100%;
    height: 50px;
  }
  .bg{
    width: 100%;
    height: 100%;
    
  }
</style>