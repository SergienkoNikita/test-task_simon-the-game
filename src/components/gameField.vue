<template>
<div class="game-field" ref="gameField">
  <div class="simon">
      <div class="tile red"
           :class="{lit: buttons[0].lit, hoverable: activeField}"
           @mousedown="clickOnBtn(buttons[0].id)"
           @mouseup="$emit('validate',buttons[0].id)"
      ></div>
      <div class="tile blue"
           :class="{lit: buttons[1].lit, hoverable: activeField}"
           @mousedown="clickOnBtn(buttons[1].id)"
           @mouseup="$emit('validate',buttons[1].id)"
      ></div>
      <div class="tile yellow"
           :class="{lit: buttons[2].lit, hoverable: activeField}"
           @mousedown="clickOnBtn(buttons[2].id)"
           @mouseup="$emit('validate',buttons[2].id)"
      ></div>
      <div class="tile green"
           :class="{lit: buttons[3].lit, hoverable: activeField}"
           @mousedown="clickOnBtn(buttons[3].id)"
           @mouseup="$emit('validate',buttons[3].id)"
      ></div>
  </div>
</div>
</template>

<script>
export default {
  name: "gameField",
  props: {sequence: Array, gameMode: String},
  data() {
    return {
      buttons: [
        {
          id: 1,
          lit: false,
        },
        {
          id: 2,
          lit: false
        },
        {
          id: 3,
          lit: false
        },
        {
          id: 4,
          lit: false
        }
      ],
      activeField: false,
    }
  },
  methods: {
    reproduceSequence (interval) {
      let i = 0;
      const animate = setInterval(() => {
        this.showBtn(this.sequence[i]);
        this.playSound(this.sequence[i]);
        i++;
        if (i >= this.sequence.length) {
          clearInterval(animate);
          this.activeField = true;
        }
      }, interval);
    },
    showBtn(id) {
      if (this.gameMode !== 'audio') {
        const currentBtn = this.buttons.find(el => el.id === id)
        currentBtn.lit = true;
        setTimeout(() => {
          currentBtn.lit = false;
        }, 300);
      }
    },
    playSound (id) {
      if (this.gameMode !== 'mute') {
        console.log('no mute')
        const currentBtn = this.buttons.find(el => el.id === id)
        const audio = new Audio(require(`../assets/audios/${currentBtn.id}.mp3`));
        audio.play();
      }
    },
    clickOnBtn(id) {
      if (this.activeField) {
        this.showBtn(id);
        this.playSound(id);
      }
    }
  }
}
</script>

<style lang="sass">
  .game-field
    grid-column: 2
    display: flex
    justify-content: center
  .simon
    position: relative
    width: 295px
    height: 290px
    border-radius: 150px

    display: flex
    flex-wrap: wrap
  .tile
    opacity: 0.6
    transition: opacity 250ms ease
    &.lit
      opacity: 1
  .red, .blue, .yellow, .green
    width: 48%
    height: 49%
    border-radius: 14px
    flex-grow: 1
  .red.hoverable:hover, .blue.hoverable:hover, .yellow.hoverable:hover, .green.hoverable:hover
    transform: scale(.98)
  .red
    background: #FF5643
    margin-right: 4px
    border-radius: 100% 14px 14px 14px
  .blue
    background: dodgerblue
    border-radius: 14px 100% 14px 14px
  .yellow
    background: #ffd400
    border-radius: 14px 14px 14px 100%
    margin-right: 4px
  .green
    background: #bfff02
    border-radius: 14px 14px 100% 14px
  .hoverable:hover
    cursor: pointer

</style>