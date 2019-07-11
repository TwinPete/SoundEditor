<template>
  <div class="sound-sketch">
      <div class="sidebar"></div>
      <AudioBoard />
  </div>
</template>

<script>
    import AudioBoard from './AudioBoard.vue'

export default {
  name: 'HelloWorld',
    components: {
        AudioBoard
    },
  props: {
    msg: String
  },
    data: function () {
        return {

        }
    },
    methods: {





    }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .sound-sketch{
      position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }

  .sidebar{
      position: fixed;
      width: 300px;
      height: 100%;
      background-color: #dae2e8;
      border-right: #c9d0d6;
  }



</style>
