<template>
  <div style="padding:5%">
    <h1>{{ msg }}</h1>
    <div style="align-text:center">
      <div style="display:inline-block;  width:35%; height:60px">
        <Multiselect v-model="value" :options="options" :searchable="true" :multiple="true" placeholder="Select characters..."></Multiselect>
        </div>
       <div>
          <button class="button button1"  v-on:click="getEpisodes" >RETRIEVE</button>
       </div>
       
    </div>
    
    <br/>
    <div style="text-align:center;">
        <CharacterPhotos :posts="posts" />
    </div> <br/>
    <div style="text-align:center; display:block; clear: Both">
        <EpisodesList :episodes="episodes" />
    </div>
  </div>
</template>

<script>

import Multiselect from 'vue-multiselect'
import EpisodesList from './EpisodesList.vue'
import CharacterPhotos from './CharacterPhotos.vue'

import axios from "axios"

export default {
  name: 'HelloWorld',
  components : {Multiselect,EpisodesList,CharacterPhotos},
  props: {
    msg: String
  },
  data () {
      return {
        value: null,
        options: [],
        posts:[],
        episodes:[]
      }
    },
    mounted  : function () {
      const baseURI = 'https://www.breakingbadapi.com/api/characters';
      axios.get(baseURI)
      .then((result) => {
       
        let chars = result.data.map( obj =>{return obj.name})
        this.options = chars;
      })
    },
    methods: {
      getEpisodes: function(){
        let characters = this.value;

        if(characters != null){
          if(typeof characters === 'string') characters=[characters];

          const baseURI = 'https://www.breakingbadapi.com/api/';

        var that = this;
          axios.all(characters.map( function(character) {
            return  axios.get(baseURI + "characters?name=" + character)
            .then((result) => {
              return result.data[0];
            })
               
            })).then(function(list){
              that.posts = list;
         });  
         

          axios.get(baseURI + "episodes")
          .then((result) => {
           
           let episodes = result.data.map(function(episode) {
            
                if(characters.every(v => episode.characters.includes(v))){
                    return episode;
                }
            })
            episodes = episodes.filter(function( element ) {
                return element !== undefined;
            });
            
            this.episodes = episodes;

              })
        }else{
          this.episodes = [];
        }
      }
    }
}
</script>
<!-- New step!
     Add Multiselect CSS. Can be added as a static asset or inside a component. -->
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 18px;
  margin: 4px 2px;
  cursor: pointer;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
}

.button1 {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
}
</style>
