<script >
    
export default {
    props: ['ep'],
    data() {
        return {
            episodeNumber: JSON.parse(this.ep.trim())["show"][0]['episodeNumber'],
            episodeName: JSON.parse(this.ep.trim())["show"][0]["episodeName"],
            description: JSON.parse(this.ep.trim())["show"][0]["description"],
            image: JSON.parse(this.ep.trim())["show"][0]["image"],
            streamURL: JSON.parse(this.ep.trim())["show"][0]["streamURL"],
            streamDuration: JSON.parse(this.ep.trim())["show"][0]["streamDuration"],
            publishedDate: JSON.parse(this.ep.trim())["show"][0]["publishedDate"],
        }
    },
    mounted: function mm(){ 
            // fucking does not work
            this.formattedEps = this.ep ;
        },
    }

</script>

<template>
  <div>
    
        <a href="{{streamURL}}">
            <div id="info">
                <div id="inner">
                    <element id="epNumber">Episode {{ episodeNumber }}</element>
                
                    <div><element id="epName">{{ episodeName }}</element></div>
                    <!-- <div><element id="epDescription">{{description}}</element></div> -->

                    <!-- <br/>:image - {{image}}
                    <br/>:streamURL - {{streamURL}}
                    <br/>:streamDuration - {{streamDuration}} -->
                    <div><element id="epDate">{{publishedDate}}</element></div>
                </div>
            </div>
        </a>
    
  </div>
</template>

<style scoped>
h1 {
    /* font-weight: 100;
    font-size: 1rem;
    top: -10px; */
    font-size: 1rem;
    /* margin-top: 50px; */
}
div #info{
    position: relative;
    /* width:84vw; */
    /* min-height: 0vh; */
    top:4px;
    left:2px;
    width:93vw;
    padding: 0.25vh 1vw 0.25vh 1vw;
    margin: 1vh 0vw 1vh 0vw;
    background-color: white;
    border-radius:2vw;
}

div #inner{
    position: relative;
    top:0px;
    width:84vw;
    height: auto;
    padding: 1vh 7vw 1vh 2vw;
    margin: 0.5vh 0px 0.5vh 0px;
    background-color:black;
    border-radius:1vw;

}

div #epNumber{
    position:relative;
    font-size: 1rem;
    top:-1vh;
    left:-3vw;
    color:white;
    background-color:rgb(139, 0, 0);
    /* border-radius: 100vh; */
    padding: 0.8vh 4vw 0.5vh 4vw;
    margin-top: 5vw;
    /* margin-bottom: 5px; */
    margin-left: 0vw;
    border-top-left-radius: 2vw;
    border-bottom-right-radius: 2vw;
}

div #epName{
    position:relative;
    font-size: 1rem;
    top:0.1vh;
    left:2vw;
    height:0.9vh;
    overflow-wrap:normal;
    color:white;
    /* border:1px; 
    border-color: black;
    border-width: 1px;
    border-style: solid; */
    /* padding: 5px 5px 5px 0px; */
    /* max-width: 5vw; */
    /* margin-top: 5vh;
    margin-bottom: 5vh;
    margin-left: 2vw;
    margin-right: 0vw; */
}

div #epDescription{
    position:relative;
    font-size: 1rem;
    top:0.5vh;
    left:2vw;
    height:1vh;
    overflow-wrap:normal;
    color:green;
    /* width: 1vw;  */
}

div #epDate{
    position:absolute;
    font-size: 0.75rem;
    top:0.5vh;
    right:3vw;
    height:1vh;
    overflow-wrap:normal;
    color:grey;
    /* width: 1vw;  */
}

h3 {
    /* border:5px; */
    border-radius: 5px;
    color: black;
    background-color: aqua;  
}
</style>
