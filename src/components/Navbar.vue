<template>
  <div id="navigation">
    <ul>
      <li @click="fetchHeadlines()">Home</li> 
      <li @click="enableEntertainment()">Entertainment</li> 
      <li @click="enableSports()">Sports</li>
      <li @click="enableTechnology()">Technology</li>
      <li @click="enableFinance()">Finance</li>
    </ul>

    <div class="search">
        <input type="text" placeholder="Search for news articles" @keydown.enter="search" v-model="query"/>
    </div>
  </div>
</template>

<script>
export default {
    name:'Navbar',
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
}
</script>

<style scoped>
#navigation {
  display: flex;
  width: 100%;
  background-color:#18181E;
  border-radius: 0px;
  height: 80px;
}

#navigation ul {
  display: flex;
}
#navigation ul li {
  font-size: 30px;
  color: #DEC79B;
  padding: 2px 8px;
  cursor: pointer;
}
 #navigation ul li:hover {
	 color: #7ca971;
}
 #navigation .search {
	 position: absolute;
	 width: 100%;
	 max-width: 350px;
   right: 50px;
   margin-top: 10px;
   background-color: #FFFFFF;
   border-radius: 10px;

}

#navigation .search input{
  outline: none;
  margin-top: 5px;
  margin-left: 20px;
  width: 100%;
  max-width: 300px;
  border-bottom-style: none;
  

}


 
</style>