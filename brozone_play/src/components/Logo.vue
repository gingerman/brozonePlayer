<script setup>

</script>

<template>
    <div id="brozoneLogoContainer">
        <img id="brozoneLogo" src="../assets/brozone_lectrocute.jpg"/>
    </div>
</template>

<style scoped>

div #brozoneLogoContainer{
  position: absolute;
  top:0;
  left:0;
  max-height: 15vh;
  width:100vw;

  aspect-ratio:calc(600/334);
  background-color: white;
  /* border-top-left-radius: 2vw;
  border-top-right-radius: 2vw; */
  border-bottom-right-radius: 2vw;
  border-bottom-left-radius: 2vw;
  z-index: 500;
}



#brozoneLogo{
  position: absolute;
  left:2vw;
  top:1vh;
  max-height: 13vh;
  aspect-ratio:calc(600/334);
  align-content: center;
}

</style>
