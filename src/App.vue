<template>
  <div class="wrapper">
    <h1>TONE <span>SYNTH</span></h1>
    <div class="optionSwitch"></div>
    <Keyboard style="margin-bottom: 100px;"/>
  </div>
</template>

<script>
import Keyboard from './components/Keyboard.vue'

export default {
  name: 'App',
  components: {
    Keyboard,
  }
}
</script>

<style scoped>
.wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
h1 {
  font-family: 'Oswald';
  font-size: 4em;
  user-select: none;
}
h1 span {
  color: dodgerblue;
}
</style>
