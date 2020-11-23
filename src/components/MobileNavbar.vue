<template>
  <div id="navigation-mobile">
      <br/>
    <div class="search">
      <input type="text" placeholder="Search for news articles" @keydown.enter="search" v-model="query"/>
    </div>
    <ul>
      <li @click="fetchHeadlines()">Home</li> 
      <li @click="enableEntertainment()">Entertainment</li> 
      <li @click="enableSports()">Sports</li>
      <li @click="enableTechnology()">Technology</li>
      <li @click="enableFinance()">Finance</li>
    </ul>
  </div>
</template>

<script>
export default {
    name:'MobileNavbar',
    data(){
      return{
        query:null,
        entertainment: false,
        sports: false,
        technology: false,
        finance: false
      }
    },
    methods:{
      search(){
          this.$emit('searchNews',this.query)
        },
        fetchHeadlines(){
          this.$root.$emit('App')
        },
        enableEntertainment(){
          this.entertainment = true
          this.$emit('entertainment',this.entertainment)
        },
        enableSports(){
          this.sports = true
          this.$emit('sports',this.sports)
        },
        enableTechnology(){
          this.technology = true
          this.$emit('technology',this.technology)
        },
        enableFinance(){
          this.finance = true
          this.$emit('finance',this.finance)
        }  
    }
};
</script>

<style scoped>

#navigation-mobile{
    height: 100vh;
    background-color: black;
}

#navigation-mobile ul{
    list-style: none;
    margin-left: 30px;
}

#navigation-mobile ul li {
	 color: #fff;
	 font-size: 2rem;
	 margin-bottom: 10px;
	 cursor: pointer;
}

#navigation-mobile .search {
    max-width: 270px;
    background-color: grey;
    border-radius: 20px;
    margin-left:20px ;
}

#navigation-mobile .search input{
    margin-top: 10px;
    margin-left: 10px;
    outline: none;
    border: none;

}

input{
    outline:none ;
}


</style>