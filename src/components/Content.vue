<template>
  <div id="content">
    <div class="container">
      <div v-for="(item,index) in pageOfItems" :key="index" class="news-display-area">
        <center>
          <div class="card">
            <a target="_blank" :href="item.url">
              <img :src="item.urlToImage" alt="Image not available">
            </a>
            <div class="container">
              <h6><b><a target="_blank" :href="item.url" style="color:white">{{item.title}}</a></b></h6> 
              <p style="color:#a9a9a9">{{item.publishedAt.slice(0,10)}}  {{item.publishedAt.slice(11,19)}} GMT</p>
              <p>{{item.description}}</p>
            </div>
          </div>
        </center>
      </div>
    </div>
    <center>
      <div class="control-area">
        <jw-pagination :disableDefaultStyles="true" :items="articles" @changePage="onChangePage" :pageSize=1 :maxPages=4 :styles="customStyles" :labels="customLabels"></jw-pagination>
      </div>
    </center>
  </div>
  
</template>

<script>

const customLabels = {
    first: '<<',
    last: '>>',
    previous: '<',
    next: '>'
};

const customStyles = {

    li: {
        display: 'inline-block',
        border: '1px solid black',
        cursor: 'pointer'
    },
};


export default {
  name: 'Content',
  props:[
    'articles'
  ],
  data () { 
    return {
      pageOfItems: [],
      customStyles,
      customLabels 
    }
  },


  methods:{
    onChangePage(pageOfItems) {
      this.pageOfItems = pageOfItems;
    }
  }
}
</script>


<style scoped>

.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 60%;
  background-color: #6B5B95;
  color: white;
  margin-bottom: 60px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}

img{
  width: 400px;
  height: 300px;
  margin-top: 20px;
  border-radius: 5px;

}

.control-area{
  position: fixed;
  bottom: 0;
  background-color: #18181E;
  height: 60px;
  width: 100%;
  border-radius: 5px;
  color: white;
}

@media only screen and (max-width:  1048px) {
  .card{
      width: 100%;
      margin-top: -20px;
  }
  img{
    width: 100%;
    height: 200px;
    margin-top: 0px;
    border-radius: 5px;
  }
}




</style>