<template>
    <div class="audio-track"
         @mousemove="translateSnippet"

    >
        <AudioSnippet
                v-bind:key="snippet.id" v-for="snippet in snippets"
                v-bind:snippet="snippet"
                v-bind:value="value"
                v-bind:isRunning="isRunning"
                v-bind:isDragging="isDragging"
                v-on:drag-start="dragStart"
                v-on:drag-end="dragEnd"
        />
    </div>
</template>

<script>
    import AudioSnippet from './AudioSnippet.vue'

    export default {
        name: "AudioTrack",
        props: ['value', 'isRunning'],
        data () {
            return {
                draggedSnippetId: '',
                isDragging: false,
                snippets: [
                    {
                        id: 'nana',
                        waveColor: '#332abc',
                        progressColor: '#8bd3ee',
                        backgroundColor: 'audioSnippetBlue',
                        startPos: 0,
                        endPos: 0,
                        duration: 0,
                        isDragged: false
                    }
                ]
            }
        },
        methods: {
            translateSnippet(event){

                // console.log(this.dragging);

                    if(this.isDragging){
                        let snippet = document.querySelector('.' + this.draggedSnippetId);
                        // console.log(event.clientX - 520);
                        const width = snippet.offsetWidth;
                        const left = snippet.offsetLeft;
                        // console.log(left);
                        if(((event.clientX - 520) - width/2) < 0){
                            return;
                        }
                        snippet.style.left = ((event.clientX - 520) - width/2) + 'px';
                        // snippet.classList.add('snippet--drag');
                    }
            },
            dragStart(id){
                this.draggedSnippetId = id;
                this.isDragging = true;
            },
            dragEnd(){
                // console.log('dragEnd');
                this.isDragging = false;
            }
        },
        mounted() {
            const snippet = document.querySelector('.nana');
            const snippetWidth = snippet.offsetWidth;
            console.log(snippetWidth);
            console.log('entfernung von links in px' + snippet.offsetLeft);
        },
        components: {
            AudioSnippet
        },
    }
</script>

<style scoped>

    .audio-track{
        position: relative;
        min-width: calc(100% - 2px);
        width: auto;
        display: flex;
        height: calc(70px - 1px);
        border-bottom: solid 2px #1d20aa;
    }


</style>