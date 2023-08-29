<template>
<div class="game-complexity">
  <h2>Сложность:</h2>
  <label >Легкая
    <input type="radio" name="complexity"  value="easy" @change="$emit('update:complexity', $event.target.value)" :checked="complexity === 'easy'">
  </label>
  <label>Средняя
    <input type="radio" name="complexity" value="medium" @change="$emit('update:complexity', $event.target.value)" :checked="complexity === 'medium'">
  </label>
  <label>Сложная
    <input type="radio" name="complexity" value="hard" @change="$emit('update:complexity', $event.target.value)" :checked="complexity === 'hard'">
  </label>
</div>
</template>

<script>
export default {
  name: "gameComplexity",
  props: {complexity: String}
}
</script>

<style lang="sass">
  .game-complexity
    grid-column: 1
    grid-row: 3
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center
    & >label
      cursor: pointer
      width: 50%
      display: flex
      justify-content: flex-end
      flex-direction: row-reverse
      align-items: center
      margin-top: 10px
      font-size: 1.4em
      & > input
        margin-right: 20px
</style>