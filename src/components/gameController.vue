<template>
<div class="game-controller">
  <button type="button" class="game-btn" @click="$emit('start')" :disabled="active || gameMode === 'free'">{{ round && active ? `Раунд ${round}` : 'Начать игру' }}</button>
  <h3 v-if="lost && gameMode !== 'free'" class="game-round">{{ `Очень жаль, вы проиграли на ${round} раунде. ${losesMsg}` }}</h3>
</div>
</template>

<script>
export default {
  name: "gameController",
  props: {round: Number, active: Boolean, lost: Boolean, gameMode: String},
  computed: {
    losesMsg : function () {
      if (this.round < 5) {
        return 'Попробуйте сменить сложность.'
      } else return 'Отличный результат!'
    }
  }
}
</script>

<style scoped lang="sass">
  .game-controller
    padding-top: 2%
    min-height: 22vh
    grid-row: 2
    grid-column: 1/4
  .game-btn
    padding: 20px 50px
    border: none
    background: #18A0FB
    border-radius: 6px
    color: #FFFFFF
    font-size: 17px
    line-height: 150%
    cursor: pointer
    transition: all .2s linear
    &:hover
      transform: scale(1.03)
    &:active
      transition: transform .1s linear
      transform: scale(.98)
    &:disabled
      background: rgba(51, 51, 51, 0)
      box-shadow: 0 0 1px 1px  #18A0FB
      cursor: default
    &:disabled:hover, &:disabled:active
      transform: none
  .game-round
    margin: 15px 0
</style>