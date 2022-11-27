<script setup>

    import { ref } from 'vue'
    import {Howl, Howler} from 'howler'

    const props = defineProps({
        show:{
            type:Object
        },
    })

    const emit = defineEmits(['clickTrackEmit'])

    let soundPlaying = false;
    let inProgress =  false;
    let sound;

    // const baseUrl = '';
    // const duration = '';
    // const name = "Track";
    // const episodeNumber = props.show.episodeNumber;  
    // const episodeName = props.show.episodeName;
    // const description = props.show.description;
    // const imageURL = props.show.image;
    // const loadmp3 = props.show.streamURL;
    // const streamDuration = props.show.streamDuration;
    // const publishedDate = props.show.publishedDate;

    function stopTrack(){
        console.log("TRACK>>stopTrack() - another track started");
        sound.stop();
        sound.seek(0);
        soundPlaying = false;
    }

    function clickTrack(){ 
        console.log( "f clickTrack" );
        // sound = new Howl();

        emit("clickTrackEmit",props.show.episodeNumber)
        var self = this;

        if ( !getInProgressStatus() ){
            console.log( "this_track_id =" + props.show.episodeNumber );

            // const trackSource =`${loadmp3}`;
            //console.log('trackSource = ' + trackSource + "\n");

            sound = new Howl({
                src: [  props.show.streamURL ],
                html5:true,
                autoUnlock:true,
                onplay: function(){
                    console.log('Playing!');
                    soundPlaying = true;
                    // Start upating the progress of the track.
                    //requestAnimationFrame(self.step.bind(self));
                },
                onload: function(){
                    //this.duration =  this.sound.duration();
                    console.log( 'Sound Loaded event'  );
                },
                onend: function(){
                    console.log('Ended!');
                },
                onpause: function(){
                    console.log('Paused!');
                },
                onstop: function(){
                    console.log('Stopped!');
                },
                onseek: function(){
                    //Start upating the progress of the track.
                    // console.log("onSeek")
                    //requestAnimationFrame(self.step.bind(self))
                },
            });

            sound.play();

            sound.onplayerror =  function() {
                sound.once('unlock', function() {
                sound.play();
                soundPlaying = true;
                });
            }


        } else {
            // console.log( 'this is at ' + this.sound.seek() );
            sound.stop();
            sound.seek(0);
            soundPlaying = false;
        };
        inProgress = !getInProgressStatus();
    }
    function getInProgressStatus(){
        return inProgress;
    }

    function seek(per) {
        var self = this;

        // Convert the percent into a seek position.
        if (sound.playing()) {
            sound.seek(sound.duration() * per);
        }
        //console.log( 'seek update ' + this.sound.duration() );
    }

    function step() {

        // Determine our current seek position.
        var seek = sound.seek() ;
        //timer.innerHTML = self.formatTime(Math.round(seek));
        // progress.style.width = (((seek / sound.duration()) * 100) || 0) + '%';

        var tim = self.formatTime(Math.round(seek));
        var perc = ((( seek / this.sound.duration()) * 100) || 0) ;
        // console.log( "percent = " + perc  +" -- " + seek)

        // TrackProgressBar.data.oldPercent = perc;
        // var pb = getElementsByClassName('.track-progress-bar');
        // pb.style.width = perc;               

        //console.log( "Track to TrackProgressBar = " + TrackProgressBar.methods.update() );
        // TrackProgressBar.data;
        // TrackProgressBar.methods.update(perc, tim)

        // If the sound is still playing, continue stepping.
        if (sound.playing()) {
        // requestAnimationFrame(self.step.bind(self));
        }
    }

    function formatTime(secs) {
        var minutes = Math.floor(secs / 60) || 0;
        var seconds = (secs - minutes * 60) || 0;

        return minutes + ':' + (seconds < 10 ? '0' : '') + seconds;
    }

</script>

<template>
    <div>
        <div id="info">
            <!-- <div id="trackContainer" v-bind="track" v-on:click=clickTrack() ></div> -->
            <div id="inner" v-on:click=clickTrack()>
                <div id="epNumber">Episode {{ props.show.episodeNumber}}
                </div>
                <div id="epName">{{ props.show.episodeName }}</div>
                <div id="epDate">{{ props.show.publishedDate }}</div>
             </div>
        </div>
    </div>
</template>

<style scoped>
div {
    position: relative;
    top:0vh;
}
div #info{
    position: relative;
    flex:auto;
    /* width:84vw; */
    min-height: 10vh;
    top:0vh;
    left:2px;
    width:93vw;
    padding: 0vh 1vw 0vh 1vw;
    margin: 0vh 0vw 1vh 0vw;
    background-color: white;
    border-radius:2vw;
}

div #infoplaying{
    background-color:red;
}

div #inner{
    position: relative;
    top:1vh;
    left:0vw;
    width:84vw;
    min-height: 8vh;
    padding: 0vh 6vw 0vh 0vw;
    margin: 0vh 0px 0vh 0px;
    background-color:black;
    border-radius:2vw;
    cursor: pointer;
}

div #info :hover{

    background-color:darkolivegreen;
}

div #epNumber{
    position:relative;
    font-size: 1rem;
    top:0vh;
    left:0vw;
    width:  15vw;
    color:white;
    background-color:red;
    padding: 0.8vh 0vw 0.5vh 4vw;
    margin-top: 0vw;
    margin-left: 0vw;
    border-top-left-radius: 2vw;
    border-bottom-right-radius: 2vw;
}

div #epName{
    position:relative;
    font-size: 1rem;
    top:0.5vh;
    left:2vw;
    min-height:0.9vh;
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
    top:0vh;
    left:2vw;
    height:1vh;
    overflow-wrap:normal;
    color:green;
    /* width: 1vw;  */
}

div #epDate{
    position:absolute;
    font-size: 0.75rem;
    top:1vh;
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
div #trackContainer{
    border-color: chartreuse;
    border-style: solid;
    width:84vw;
    height: auto;
    background-color: chartreuse;
    z-index: 100;

}
</style>
