<template>
    <div class="audio-snippet"
         @mousedown="$emit('drag-start', snippet.id)"
         @mouseup="$emit('drag-end', snippet.id)"
         v-bind:class="[snippet.backgroundColor, snippet.id, {isDragged: isDragging}]"
         v-if="value >= 10"
    ></div>
</template>

<script>
    import WaveSurfer from 'wavesurfer';

    export default {
        name: "AudioSnippet",
        props: ['snippet', 'value', 'isRunning', 'isDragging'],
        watch: {
            isDragging: function(newVal, oldVal){
                console.log('Prop changed: ', newVal, ' | was: ', oldVal);
            },
            value: function(newVal) { // watch it
                // console.log('Prop changed: ', newVal, ' | was: ', oldVal);
                // console.log(this.snippet.startPos);
                if(newVal >= this.snippet.startPos && newVal <= this.snippet.endPos && this.isRunning){
                    if(this.wavesurfer.isPlaying()){
                        return;
                    }else{
                        this.play();
                    }
                }
                if(newVal > this.snippet.endPos){
                    this.pause();
                }
            },
            isRunning: function(newVal){
                if(newVal == false){
                    console.log('hat gestoppet');
                    console.log('wavesurfer spielt: ' + this.wavesurfer.isPlaying());
                    if(this.wavesurfer.isPlaying()){
                        console.log('inside the func');
                        // this.stop();
                        this.wavesurfer.pause();
                    }
                }
            }
        },
        methods: {
            setSnippetAttributes(){
                let dur = this.wavesurfer.backend.buffer.duration;
                console.log('duration of snippet: ' + dur);
                this.snippet.duration = dur * 1000;
                let r = document.querySelector("#time");

                const snippet = document.querySelector('.nana');
                this.snippet.startPos = (snippet.offsetLeft - 220) / 0.021916666666666668;
                console.log('startPos bei: ' + this.snippet.startPos);
                this.snippet.endPos = this.snippet.startPos + this.snippet.duration;
                console.log('endPos bei: ' + this.snippet.endPos);
            },
            dragStart(){
                this.snippet.isDragged = true;

            },
            dragEnd(){
                this.snippet.isDragged = false;
            },
            play() {
                this.wavesurfer.play(((this.value - this.snippet.startPos)/1000), this.snippet.duration);
            },
            stop() {
                this.wavesurfer.pause();
            },
            getDur(){
                console.log(this.wavesurfer.getDuration());
                console.log(this.wavesurfer);
            }
        },
        created (){
            console.log('created');
        },
        beforeMount(){
            console.log('beforeMount');
        },
        mounted () {
            console.log('mounted');


            this.wavesurfer = WaveSurfer.create({
                container: '.' + this.snippet.id,
                height: 70,
                waveColor: this.snippet.waveColor,
                progressColor: this.snippet.progressColor
            });
            this.wavesurfer.load("https://upload.wikimedia.org/wikipedia/commons/6/6e/Micronesia_National_Anthem.ogg")
            console.log(this.wavesurfer);




            setTimeout(() => {

                let dur = this.wavesurfer.backend.buffer.duration;
                console.log('duration of snippet: ' + dur);
                this.snippet.duration = dur * 1000;
                let r = document.querySelector("#time");

                const snippet = document.querySelector('.nana');
                this.snippet.startPos = (snippet.offsetLeft - 220) / 0.021916666666666668;
                console.log('startPos bei: ' + this.snippet.startPos);
                this.snippet.endPos = this.snippet.startPos + this.snippet.duration;
                console.log('endPos bei: ' + this.snippet.endPos);



            }, 1000);


            console.log('value: ' + this.value);



        },
        update(){



        }
    }
</script>

<style scoped>

    .audio-snippet{
        position: absolute;
        width: 730.167658px;
        /*width: 78.193px;*/
        height: calc(100% - 2px);
        border-radius: 10px;
        left: 100px;
    }

    .audioSnippetBlue{
        background-color: #fff;
        border: solid 2px #1d20aa;
    }

    .audioSnippetRed{
        background-color: #bc443e;
        border: solid 1px #ad3f39;
    }
    .isDragged{
        cursor: grabbing;
    }

</style>