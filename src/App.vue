<template>
  <div class="container">
    <h1>Reaction Timer</h1>

    <button v-if="playing === false" @click="stateGame()" :disabled="playing">Play</button>
    <button v-else @click="stateGame" :disabled="!playing">One Again</button>

    <Results v-if="showResult" :results="reactionTime"/> 
    <Block v-if="playing === true" :delay="delay" @end="endGame"/>
  </div>

  <div class="footer">
    <p>Created by Dawid Polak</p>  
  </div>

</template>

<script>
  import Block from './components/Block.vue';
  import Results from './components/Results.vue'

  export default {
    name: 'App',
    components: {
      Block,
      Results
    },
    data() {
      return {
        playing: false,
        delay: null,
        reactionTime: null,
        showResult: false
      }
    },
    methods: {
      stateGame() {
        this.playing = !this.playing;
        this.delay = 2000 + Math.random() * 6000;
        this.showResult = false;
      },
      endGame(e) {
        this.reactionTime = e;
        this.showResult = true
        this.playing = false
      }
    }
  }
</script>

<style>
  body {
      margin: 0;
      padding: 0;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .container button {
    padding: 10px;
    color: #2c3e50;
    background-color: #42d392;
    border: 0px;
    border-radius: 5px;
    width: 100px;
    height: 40px;
  }

  .container button:hover {
    cursor: pointer;
    box-shadow: #2c3e50 0px 0px 4px 0px;
  }

  .container button:active {
    transform: translateY(1px);
  }

  .footer {
    position: absolute;
    bottom: 0;
    width: 100vw;
    background-color: #42d392;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .footer p {
    margin: 0px;
    padding: 0px;
    font-size: 10px;
    font-weight: 700;
  }
</style>
