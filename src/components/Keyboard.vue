<template>
  <div class="keyboard">
    <div class="key white" v-for="key in keyList" :key="key" @click="toggleTone(key.note)" :class="{ active: currentNote === key.note }">
      <p>{{ key.noteLabel }}</p>
      <div v-if="key.black" class="key black" @click.stop="toggleTone(key.black.note)" :class="{ active: currentNote === key.black.note }"></div>
    </div>
  </div>
</template>

<script>
import * as Tone from 'tone'

export default {
  name: 'Keyboard',
  data() {
    return {
      stopSynth: () => {},
      playing: false,
      currentNote: '',
      keyList: [
        {
          type: 'white',
          note: 'F3',
          noteLabel: 'F',
          black: { note: 'F#3' },
        },
        {
          type: 'white',
          note: 'G3',
          noteLabel: 'G',
          black: { note: 'G#3' },
        },
        {
          type: 'white',
          note: 'A3',
          noteLabel: 'A',
          black: { note: 'A#3' },
        },
        {
          type: 'white',
          note: 'B3',
          noteLabel: 'B',
        },
        {
          type: 'white',
          note: 'C4',
          noteLabel: 'C',
          black: { note: 'C#4' },
        },
        {
          type: 'white',
          note: 'D4',
          noteLabel: 'D',
          black: { note: 'D#4' },
        },
        {
          type: 'white',
          note: 'E4',
          noteLabel: 'E',
        },
        {
          type: 'white',
          note: 'F4',
          noteLabel: 'F',
          black: { note: 'F#4' },
        },
        {
          type: 'white',
          note: 'G4',
          noteLabel: 'G',
          black: { note: 'G#4' },
        },
        {
          type: 'white',
          note: 'A4',
          noteLabel: 'A',
          black: { note: 'A#4' },
        },
        {
          type: 'white',
          note: 'B4',
          noteLabel: 'B',
        },
        {
          type: 'white',
          note: 'C5',
          noteLabel: 'C',
        },
      ],
    }
  },
  methods: {
    async toggleTone(note) {
      if (this.playing) {
        this.stopSynth()
        this.playing = false
        if (this.currentNote === note) {
          this.currentNote = ''
          return
        }
      }
      const synth = new Tone.Synth().toDestination()
      synth.triggerAttack(note, undefined, 1.5)
      this.stopSynth = () => synth.triggerRelease()
      this.playing = true
      this.currentNote = note
    },
  },
  async mounted() {
    // Loading?
    await Tone.start()
  },
}
</script>

<style scoped>
.keyboard {
  display: flex;
  flex-direction: row;
  transform: perspective(300px) rotateX(12deg) scale(1.1);
  transform-style: preserve-3d;
}
.key {
  cursor: pointer;
  transition: 0.3 cubic-bezier(0,0,.2,1);
}
.white {
  background-color: #FFFFFF;
  height: 160px;
  width: 70px;
  color: rgb(117, 117, 117);
  border: 1px solid black;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  border-radius: 5px;
}
.white:hover {
  background: orange;
}
.key p {
  margin: 0 0 10px 0;
  padding: 0;
  font-weight: bold;
  user-select: none;
}
.black {
  background-color: #000000;
  height: 80px;
  width: 40px;
  z-index: 10;
  position: absolute;
  top: 0;
  right: -20px;
}
.black:hover {
  background: rgb(255, 128, 0);
}
.white.active { background-color: orange; }
.black.active { background-color: rgb(255, 128, 0); }
</style>