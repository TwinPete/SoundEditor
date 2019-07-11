<template>
    <div class="audio-board">
        <div class="optionbar">
            <div class="watch-controls">
                <div class="start"></div>
                <div class="pause"></div>
                <div class="stop"></div>
                <div class="led">
                    <div class="led__light" v-bind:class="{ ledActive: isRunning }"></div>
                </div>
            </div>
        </div>
        <div class="track-board">
            <div class="controls-frame">
                <div class="head">
                    <div class="watch" @click="startWatch"> {{ watch }} </div>
                </div>
                <AudioControls />
            </div>
            <div class="tracks-frame">
                <div class="tracks-wrapper">
                    <div class="timeline">
                        <input id="time" type="range" name="points" min="0" max="60000"  @change="show" v-model="value">
                    </div>
                    <AudioTrack
                            v-bind:value="value"
                            v-bind:isRunning="isRunning"
                            v-bind:key="audioTrack.id" v-for="audioTrack in audioTracks"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import AudioTrack from './AudioTrack.vue'
    import AudioControls from './AudioControls.vue'


    export default {
        name: "AudioBoard",
        components: {
            AudioTrack,
            AudioControls
        },
        data() {
            return{
                isRunning: false,
                // value: 4889.97555,
                value: 3000,
                // time: {
                //     hours: 0,
                //     minutes: 0,
                //     seconds: 0,
                //     milliseconds: 0
                // },
                watch: '00:00:00:00',
                audioTracks: [
                    {
                        id: 1
                    }

                ]
            }
        },
        methods: {
            show(){
                console.log('milliseconds: ' + this.value);

                console.log('time: ' + this.msToTime(this.value));
                this.watch = this.msToTime(this.value);
            },
            msToTime(duration) {

                if(duration == 0){
                    return '00:00:00:00';
                }

                var milliseconds = parseInt((duration%1000)/100),
                    seconds = parseInt((duration/1000)%60),
                    minutes = parseInt((duration/(1000*60))%60),
                    hours = parseInt((duration/(1000*60*60))%24);

                    hours = (hours < 10) ? "0" + hours : hours;
                    minutes = (minutes < 10) ? "0" + minutes : minutes;
                    seconds = (seconds < 10) ? "0" + seconds : seconds;
                    milliseconds = (milliseconds < 10) ? "0" + milliseconds : milliseconds;

                let time = hours + ":" + minutes + ":" + seconds + "." + milliseconds;
                return String(time);
            },


            startInterval(id){
                let range = document.querySelector("#time");
                let value = parseInt(range.value);

                console.log(this.isRunning);

                if(value > 60000 - 10 || this.isRunning == false){
                    console.log('watch finished');
                    clearInterval(id);
                    console.log(this.value);
                    this.isRunning = false;
                }

                range.value = value + 10;
                this.value = value + 10;
                // console.log(this.value);

                this.watch = this.msToTime(range.value);
                // console.log(this.watch);
            },

            startWatch(){

                if(!this.isRunning){
                    this.isRunning = true;
                    let interval = setInterval(() => {
                        this.startInterval(interval);
                    }, 10);
                }else{
                    this.isRunning = false;
                }




            }
        },
        mounted () {

                const element = document.querySelector('#time');
                console.log(element);
                const style = element.offsetWidth;
                console.log('Width of Timeline in Px: ' + style);
                let oneMilisecond = style / 60000;
                console.log('kleiste Maseinheit ist: ' + oneMilisecond);
                console.log('entfernung von links in px' + element.offsetLeft);




            // this.counter();

        }
    }
</script>

<style scoped>

    .audio-board{
        position: absolute;
        top: 200px;
        right: 0;
        display: flex;
        flex-direction: column;
        margin-top: 30px;
        width: calc(100% - 300px);
        max-height: 440px;
        border: solid 1px #1d20aa;
        overflow: scroll;
        background-color: #fff;
    }
    .optionbar{
        height: 30px;
        min-width: 100%;
        background-color: #1d20aa;
        border-bottom: solid 1px #1d20aa;
    }
    .watch-controls{
        width: 220px;
        height: 100%;
        border-right: solid 1px #1d20aa;
        display: flex;
    }
    .start, .pause, .stop, .led{
        width: 25%;
        height: 100%;
        border-right: solid 1px #1d20aa;
    }
    .led{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .led__light{
        width: 20px;
        height: 20px;
        border-radius: 50%;
        background-color: #555;
    }
    .ledActive{
        background-color: #ff2d54 !important;
    }
    .track-board{
        width: 100%;
        display: flex;
    }
    .tracks-frame{
        display: flex;
        flex-direction: column;
        min-width: calc(100% - 220px);
        overflow-x: scroll;
        align-items: flex-start;
    }
    .tracks-wrapper{
        min-width: 100%;
    }
    .timeline{
        display: flex;
        align-items: centeR;
        height: 30px;
        width: 100%;
        justify-content: flex-start;
        background-color: #f4f4f4;
    }

    .timeline input{
        display: block;
        width: 100%;
    }

    .head{
        height: 30px;
        width: 100%;
        background-color: #1d20aa;
        border-bottom: solid 1px #1d20aa;
        border-right: solid 1px #1d20aa;
    }

    .watch{
        color: #fff;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

</style>