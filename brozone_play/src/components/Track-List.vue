<script setup>

      import { ref, watchEffect } from 'vue'
      import Track from './Track-Comp.vue'
      /// static data be static data - right !
      // import brozones from '../assets/data'
      import axios from 'axios'

      const dataURL = '/data.json';
      //   export default {    emits: ['accepted']
      //   }

      // const props = defineProps({
      //       loaded:{
      //       type:Boolean,
      //       value:false
      //   },
      // })

      let loaded = ref(true);
      let broData = ref(null); //= ref(brozones);


      watchEffect(async () => {
            // this effect will run immediately and then
            // re-run whenever currentBranch.value changes
            const url = `${dataURL}`
            broData.value = await (await fetch(url)).json()
      })

      // const sexy = () => {
      //       axios.get(dataURL)
      //       .then(function (response) {
      //             console.log("/ngot data/ngot data/ngot data ?");
      //             loaded = true;
      //             broData = response;
      //       })
      //       .catch ( error =>{
      //             loaded = false
      //             console.log(error)
      //       })
      // }

      let currentlyPlayingID = 0;

      // sexy();


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
      
      <div class="trackList" >
            <Track  v-for="show in broData.slice().reverse()" 
            :key="show.episodeNumber"
            :show="show"
            @id="stopOtherTracksNotThis(show.id)"></Track>
      </div>

      <!-- slice().reverse() -->
      <!-- <div class="spinnerContainer">
            <div v-if="!loaded" class="spinner" />
      </div> -->
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

 /*     .spinnerContainer{
            margin-left: 45vw;
            margin-right: 45vw;
            width:100vw;
            height:100vh;
      }
      .spinner {
            width: 56px;
            height: 56px;
            display: grid;
            animation: spinner-plncf9 4s infinite;
      }
 
      .spinner::before,
      .spinner::after {
            content: "";
            grid-area: 1/1;
            border: 9px solid;
            border-radius: 50%;
            border-color: #ebf304 #d74b13 rgba(85, 22, 4, 0) #0000;
            mix-blend-mode: darken;
            animation: spinner-plncf9 1s infinite linear;
      }

      .spinner::after {
            border-color: #0000 #0000 #ff0000 #dbdcef;
            animation-direction: reverse;
      }

      @keyframes spinner-plncf9 {
            100% {
                  transform: rotate(1turn);
            }
      } */
</style>