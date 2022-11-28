<script setup>

      import { ref } from 'vue'
      import Track from './Track-Comp.vue'
      /// static data be static data - right !
      import brozones from '../assets/data'
      import axios from 'axios'


      //   export default {    emits: ['accepted']
      //   }

      // const brozones = async =>() {
      //       const {data} = await axios.get('/posts')
      //       return {articles:data}
      // }
      var loaded = true;
      let broData = brozones;
      //let brozones;

      // const post = await fetch(`http://localhost:5173/brozone/`,{ mode:'no-cors',}).
      //       then( ( respnse ) => {
      //             console.log("got data ?");
      //             loaded = false;
      //             brozones = response.json();
      //             response.json()
      //       }).catch ( error =>{
      //             this.loading = false
      //             console.log(error)
      //       })

      ///
      //////
      ///

      const sexy = () => {
            axios.get('./data.json')
            .then( Response =>{
                  console.log("got data ?");
                  loaded = false;
                  broData = response.data;
            })
            .catch ( error =>{
                  loaded = false
                  console.log(error)
            })
      }

      let currentlyPlayingID = 0;

      sexy();


      function  stopOtherTracksNotThis(value) {
            console.log("\n\nstopOtherTracksNotThis track = "+value);
            if (currentlyPlayingID==0){
            console.log("ID NOT SET value = " + value);
            currentlyPlayingID = value;
            } else {
            console.log("ID SET value = " + value);
            // stop currently playing ID
            Track[value].stopTrack();
            // update currently playing
            currentlyPlayingID = value; 
            }
      }
</script>

<template >
      <div class="spinner" v-if="loaded===false"> loading</div>
      <div class="trackList" v-else>
      <!-- <Track v-for="show in brozones.slice().reverse()"  -->
            <Track v-for="show in brozones.slice().reverse()" 
            :key="show.episodeNumber"
            :show="show"
            @id="stopOtherTracksNotThis(show.id)"></Track>
      </div>
</template>

 <!-- :ep = "JSON.stringify(show)"> -->

<style scoped>
       /* template{
      position: absolute;
      top:13vh;
      } */
      div .trackList{
      position: relative;
      top: 13vh;
      width: 85vw;
      height: 50vh;
      }
</style>
