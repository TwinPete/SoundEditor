<template>
    <div class="audio-track__controls">
        <div class="control"></div>
        <div class="control"></div>
        <div class="control"></div>
    </div>
</template>

<script>
    export default {
        name: "AudioControls",


    }
</script>

<style scoped>

    .audio-track__controls{
        display :flex;
        flex-direction: column;
        width: 220px;
    }



    .control{
        height: calc(70px - 1px);
        width: 100%;
        background-color: #1d20aa;
        border-bottom: solid 1px #191b92;
        border-right: solid 1px #171985;
        border-radius: 2px;
    }


</style>