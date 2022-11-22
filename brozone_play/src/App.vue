<script setup>
import TrackList from './components/TrackList.vue';
import Logo from './components/Logo.vue';

// const trackList = "hi";
</script>

<template>

  <div id="trks">
    <TrackList></TrackList>
  </div>
  <div id="lgo">
  <Logo></Logo>
  </div>
</template>

<style scoped>

div #lgo{
  position: fixed;
  top:0;
  left: 0;
}

div #trks{

  position: absolute;
  top:4vh;
  left:1vw;
  overflow:visible;
  min-height: 100vh;

}

h1{
  color: red;
  border: 1px;
  border-color: yellow;
  border-style: solid;
  padding: 10px;
  margin: 2px;
  
}
main {

  color: cyan;
  border: 1px;
  border-color: yellow;
  border-style: none;
  background-color: gray;
  padding: 10px;
  margin-top: 5px;
}

</style>
