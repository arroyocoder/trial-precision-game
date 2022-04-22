<template>
<div>
  <h1>Reflex Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <!--disabled html atributte in bided to isPlaying data property so the button is disabled when the block show up, therefore is not posible to start a new game while the game is playing-->
  <!-- the button above click-fires a function called start declared in our methods. The function change two parametres
  of our data properties (isPlaying and delay) -->

  <!--BLOCK COMPONENT-->
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <!-- Block component only shows if the property isPlaying is set to true-->
  <!--END OF BLOCK COMPONENT-->
  <Result v-if="showResult" :score="score" />
  <!--Result component only shows when the showResult property is true. false at start(), true at endGame())-->
  </div>
</template>

<script>
//Components step 1: import component from dedicated folder
import Block from "./components/Block.vue";
import Result from "./components/Result.vue";

export default {
  name: "App", //App name of choice
  //Components step 2: declare components
  components: { Block, Result },
  data() {
    return {
      isPlaying: false,
      delay: null, //this store the delay info from the start() method
      score: null,
      showResult: false,
    };
  },
  methods: {
    //Game start, delay start increasing reaction time.
    start() {
      this.delay = 2000 + Math.random() * 5000; // this declaration sets the delay property to random gamount of miliseconds between 2 and 5 seconds
      this.isPlaying = true; //in here the data property "isPlaying" is set to true
      this.showResult = false;
    },
    //End of game, reactionTime custon event add value to score. The Result component is then shown and returned to false when start() is executed
    endGame(reactionTime) {
      this.score = reactionTime;
      this.showResult = true;
      this.isPlaying = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
</style>
