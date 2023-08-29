<template>
<div class="game-settings">
  <h2>Режим:</h2>
  <label >Стандартный
    <input type="radio" name="game-mode"  value="normal" @change="$emit('update:gameMode', $event.target.value)" :checked="gameMode === 'normal'">
  </label>
  <label>Без звука
    <input type="radio" name="game-mode" value="mute" @change="$emit('update:gameMode', $event.target.value)" :checked="gameMode === 'mute'">
  </label>
  <label>Только звук
    <input type="radio" name="game-mode" value="audio" @change="$emit('update:gameMode', $event.target.value)" :checked="gameMode === 'audio'">
  </label>
  <label>Свободный
    <input type="radio" name="game-mode" value="free" @change="$emit('update:gameMode', $event.target.value)" :checked="gameMode === 'free'">
  </label>
</div>
</template>

<script>
export default {
  name: "gameSettings",
  props: {gameMode: String}
}
</script>

<style lang="sass">
  .game-settings
    grid-column: 3
    grid-row: 3
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center
    & >label
      cursor: pointer
      width: 70%
      display: flex
      flex-direction: row
      justify-content: flex-end
      align-items: center
      margin-top: 10px
      font-size: 1.4em
      & > input
        margin-left: 20px

</style>