<template>
  <div id="app">
    
    <MobileNavbar 
      v-on:searchNews="searchAndSendNews($event)"
      v-on:entertainment="searchAndSendEntertainmentNews($event)"
      v-on:sports="searchAndSendSportsNews($event)"
      v-on:technology="searchAndSendTechnologyNews($event)"
      v-on:finance="searchAndSendFinanceNews($event)"
    />


    <div class="main-div" :class="{'open':showNav}">
      <div class="top-bar">
        <div id="navigation-icon" v-if="mobileView" @click="showNav = !showNav">
          <i class="fas fa-bars"></i>
        </div>
        
        <Navbar v-if="!mobileView" 
          v-on:searchNews="searchAndSendNews($event)" 
          v-on:entertainment="searchAndSendEntertainmentNews($event)"
          v-on:sports="searchAndSendSportsNews($event)"
          v-on:technology="searchAndSendTechnologyNews($event)"
          v-on:finance="searchAndSendFinanceNews($event)"
        />
      </div>
      <br/>
      <Content :articles="articles"/>

    </div>
  </div>
</template>

<script>

import Navbar from '@/components/Navbar'
import MobileNavbar from '@/components/MobileNavbar'
import Content from "@/components/Content"

export default {
  name:'App',
  data() {
    return {
      mobileView: true,
      showNav: false,
      searchQuery: null,
      articles:{},
      api_key: '42eafba805074d68a0a26a94453c2992',
      url_base: 'http://newsapi.org/v2/',
      country: 'in',
      query:null
    };
  },

  mounted(){
    this.$root.$on('App', () => {
      this.fetchHeadlines()
    })
    this.fetchHeadlines()
  },


  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 1048;
    },

    fetchHeadlines(){
            this.showNav = false

        fetch(`${this.url_base}top-headlines?sortBy=publishedAt&country=${this.country}&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        });
    }, 

    searchAndSendNews(query){
      this.showNav = false
      this.query = query
      fetch(`${this.url_base}everything?sortBy=publishedAt&q='${this.query}&'&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        })
        .catch(err=>{
          alert("No article found for the entered term")
        });
    },

    searchAndSendEntertainmentNews(entertainment){
      this.showNav = false
      if(entertainment){
        console.log(`${this.url_base}top-headlines?sortBy=publishedAt&category=entertainment&country=in&apiKey=${this.api_key}`)
        fetch(`${this.url_base}top-headlines?sortBy=publishedAt&category=entertainment&country=in&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        })
        .catch(err=>{
          alert("No article found for the entered term")
        });
      }
    },

    searchAndSendSportsNews(sports){
      this.showNav = false
      if(sports){
        fetch(`${this.url_base}top-headlines?category=sports&country=in&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        })
        .catch(err=>{
          alert("No article found for the entered term")
        });
      }
    },

    searchAndSendTechnologyNews(technology){
      this.showNav = false
      if(technology){
        fetch(`${this.url_base}top-headlines?category=technology&country=in&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        })
        .catch(err=>{
          alert("No article found for the entered term")
        });
      }
    },

    searchAndSendFinanceNews(finance){
      if(finance){
        this.showNav = false
        fetch(`${this.url_base}top-headlines?category=business&country=in&apiKey=${this.api_key}`)
        .then(response => response.json())
        .then(data => {
          this.articles = data.articles
        })
        .catch(err=>{
          alert("No article found for the entered term")
        });
      }
    }
  },
  components: {
    Navbar,
    Content,
    MobileNavbar
  },
  created() {
    this.handleView();
    window.addEventListener('resize', this.handleView);
  }
};
</script>

<style scoped>
@import url("https://use.fontawesome.com/releases/v5.9.0/css/all.css");


 #app {
	 position: absolute;
	 width: 100%;
	 height: 100vh;
	 color: #333;
	 overflow: visible;
}
 .top-bar {
	 display: flex;
	 width: 100%;
}
 #navigation-icon {
	 padding: 10px 10px 20px;
	 margin-right: 10px;
	 cursor: pointer;
}
 #navigation-icon i {
	 font-size: 2rem;
}
 .main-div {
	 position: absolute;
	 top: 0px;
	 width: 100% ;
	 height: 100vh;
	 background-color:#DEC79B;
	 transition: 1s transform cubic-bezier(0, 0.12, 0.14, 1);
}
 .open {
	 transform: translateX(300px);
}
 
</style>