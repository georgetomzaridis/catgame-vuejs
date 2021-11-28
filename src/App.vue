<template>
  <h2>Cat Game</h2>
  <h3>Created by <a href="https://georgetomzaridis.eu">George Tomzaridis</a> for fun in VueJS</h3>
  <p>This game is about cats. Got that?</p>
  <p>When you press start I will show you <b>{{ images_given }} cat images</b> and you have <b>{{ time_require_each }} seconds for each picture</b> before hide it and move on.</p>
  <p>In the end you need to write down how many cats appear.</p>
  <br>
  <p><b>Be careful! Good luck!!</b></p>
  <button v-if="!isPlaying" @click="startGame">Start game</button>
  <br>
  <div style="margin: 2em 0;">
    <Game v-if="isPlaying" :image_given="images_to_show" :switch_time="time_require_each" :isPlaying="isPlaying" :total_cats_answer="total_cats_answer"/>
  </div>

  
  
</template>


<script>

import Game from './components/Game.vue';
import json_db from './cat-db.json';

export default {
  name: 'App',
  components: {
    Game
  },
  methods: {
    generateGame: function(){
      this.time_require_each = this.randomIntFromInterval(1, 3);
      var total_db_count = json_db.length;
      var img_arr_br = this.images_to_show;
      console.log(json_db[0].image);

      for(var a = 0; a <= this.randomIntFromInterval(2, (total_db_count - 1)); a++){
       var randselectarr = this.randomIntFromInterval(0, (total_db_count - 1))
       if(img_arr_br.indexOf(json_db[randselectarr].image) === -1){
         img_arr_br.push(json_db[randselectarr].image);
         this.total_cats_answer += json_db[randselectarr].count;
       }
      }

      this.images_given = img_arr_br.length;
    },

    startGame: function(){
      this.isPlaying = true;
    },

    randomIntFromInterval: function (min, max) { 
      return Math.floor(Math.random() * (max - min + 1) + min)
    }
  },

  data(){
    return {
      isPlaying: false,
      images_given: null,
      time_require_each: null,
      total_cats_answer: null,
      images_to_show: []
    }
  },

  beforeMount(){
    this.generateGame()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
