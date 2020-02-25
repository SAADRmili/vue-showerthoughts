<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <full-page :options="options" id="fullpage" v-if="isLoaded">
            <div v-for="sh in shower" :key="sh.data.id" class="section">
              <div class="container">
                <img src="./assets/hair.png" alt="shower icon" width="20%" height="20%">
               
              
                <div class="quote-symbol">
                  "
                </div>
                <p class="quote"><a :href="sh.data.url">{{ sh.data.title }}</a></p>
                <div class="details-author">
                  Author : {{ sh.data.author_fullname }}
                </div>

                <div class="stats">{{ sh.data.ups }} Upvote | {{ sh.data.num_comments }} comments</div>
              </div>
            </div>
        
        </full-page>
        <div v-else>
          <loading></loading>
        </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Loading from './components/Loding.vue'
export default {

  name: 'App',
  components: {
  //  HelloWorld
   Loading,
  },

  created()
  {
    fetch('https://www.reddit.com/r/showerthoughts.json?limit=20').then(response=>response.json()).then(data=>{
     this.shower = data.data.children;
     this.shower.shift();
     this.shower.shift();
     this.isLoaded=true;
    });
  },
   data () {
      return {
        isLoaded : false,
        shower:[],
        options: {
         
          afterLoad: this.afterLoad,
          
          navigation: true,
          
          sectionsColor: ['#41b883', '#ff5f45', '#0798ec', '#fec401', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab', '#0798ec', '#fec401', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab']
        }
      }
    },


}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");
  #app {
    font-family:sans-serif;
    color: #2d3748;

  }

  body{
    margin: 0;
    padding: 0;
  }

  h3{
    margin: 0;
  }

  .container{
    margin: auto;
    max-width: 800px;
    padding: 80px 16px;
  }
  .section{
    text-align: center;
  }

  .quote-symbol{
    font-size: 64px;
    line-height: 0;
    margin-top: 50px;
    color: white;  }

    .quote a{
      text-decoration:  none;
      font-family: 'Sriracha',cursive;
      color: white;
      font-size: 36px;
      line-height: 1.5;
    }

    .quote a:hover{
      color: #edf2f7;
    }

    .details-stats{
      margin-top: 4px;
    }

</style>
