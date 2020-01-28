<template>
<div class="search-box">
  <input type="text" v-model="term" v-on:keyup.enter="searchGiphy()" />
  <button class="float-right" variant="primary" @click="searchGiphy()">Search</button>

</div>


  <b-card-group columns>
    <b-card
     v-for="gif in gifs"
     :key="gif.id"
     :img-src="gif.images.fixed_width.url"
     :img-alt="gif.title"
     >
     <b-card-text>
       <a :href="gif.url" target="_blank"> {{gif.title}}</a>
     </b-card-text>
    </b-card>
  </b-card-group>
</template>

<script>
/* eslint-disable no-console */
import axios from 'axios';

const GIPHY_URL = "https://api.giphy.com/v1/gifs"
const API_KEY = "DyDClUSMLgq5iZPz6QqmFzixtI1p6ZuE"

export default {
  name: "GiphyViewer",
  components:{

  },
  data(){
    return{
      gifs:[],
      term:''
    };
  },
  mounted() {
   axios.get(`${GIPHY_URL}/trending?api_key=${API_KEY}`)
        .then(response => {
          this.gifs = response.data.data
        })
        .catch(error => console.log(error));
  },
  methods:{
searchGiphy(){
  if(!this.term){
    alert("please enter a search term!");
    return;
    }
    axios.get(`${GIPHY_URL}/search?api_key=${API_KEY}&q=${this.term}&limit=20`)
         .then(response => {
           this.gifs = response.data.data
    })
         .catch(error => console.log(error));
   },
   showTrending(){

   }
  }
};
</script>

<style>
.seach-box{
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
