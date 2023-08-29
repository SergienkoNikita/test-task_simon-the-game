<template>
<div class="container">
  <div class="game">
    <h1>&laquo;Simon The Game&raquo;</h1>
    <game-controller
      :round="round"
      :active="active"
      :lost = 'lost'
      :gameMode="gameMode"
      v-on:start="startGame"
    />
    <game-complexity
        :complexity.sync="complexity"
    />
    <game-settings
        :gameMode.sync="gameMode"
    />
    <game-field
      :sequence="sequence"
      :gameMode="gameMode"
      v-on:validate="validateSequence($event)"
      ref="gameField"
    />
  </div>
</div>
</template>

<script>
import gameController from "./gameController";
import gameComplexity from "./gameComplexity";
import gameSettings from "./gameSettings";
import gameField from "./gameField";


export default {
  name: "Game",
  components: {gameController,gameComplexity, gameSettings, gameField},
  data() {
    return  {
      round: 0,
      active: false,
      complexity: 'easy',
      gameMode: 'normal',
      sequence: [],
      lost: false
    }
  },
  methods: {
    startGame() {
      this.round = 0
      this.active = true;
      this.lost = false;
      this.sequence = [];
      this.createNewRound();
    },
    createNewRound() {
      this.round++;
      this.sequence.push(this.getRandomNum());
      this.$refs.gameField.reproduceSequence(this.interval);
    },
    getRandomNum() {
      return  Math.floor((Math.random()*4)+1)
    },
    validateSequence(id) {
      if (this.$refs.gameField.activeField && this.gameMode !== 'free') {
        const currentVal = this.cacheSequence.shift();
        if (id === currentVal && this.cacheSequence.length === 0) {
          this.$refs.gameField.activeField = false;
          setTimeout(()=>{this.createNewRound()}, 500)
        } else if (id !== currentVal) {
          this.$refs.gameField.activeField = false;
          this.stopGame();
        }
      }
    },
    stopGame() {
      this.active = false;
      this.lost = true;
    }
  },
  computed: {
    interval: function () {
      if (this.complexity === 'easy') {
        return 1500
      } else if (this.complexity === 'medium') {
        return 1000
      } else return 400
    },
    cacheSequence: function () {
      return this.sequence.slice(0)
    }
  },
  watch: {
    gameMode(val) {
      if (val === 'free') {
        this.stopGame();
        this.lost = false;
        this.round = 0
        this.$refs.gameField.activeField = true;
      }
    }
  }
}
</script>

<style scoped lang="sass">
  .container
    max-width: 1200px
    margin: 0 auto
  .game
    display: grid
    grid-template-columns: 25% 50% 25%
    width: 100%
    padding: 5%
    align-items: start
    & > h1
      grid-column: 1/4
</style>