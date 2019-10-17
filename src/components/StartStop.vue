<template>
  <div>
  <button v-on:click="start" v-bind:disabled="status === 'work'" >Start working</button>
  <button v-on:click="stop" v-bind:disabled="status === 'break'" >Take a break</button>
  <button v-on:click="pause" v-bind:disabled="status === 'pause'" >Stop the clock</button>
  </div>
</template>

<script>
export default {
  name: 'StartStop',
  props: {
    status: String
  },
  methods: {
    start: function () {
      this.$emit('start')
    },
    stop: function () {
      this.$emit('stop')
    },
    pause: function () {
      this.$emit('pause')
    }
  }
}
</script>

<style lang="scss" scoped>
// button{
//   border: 2px solid #272932;
//   cursor: pointer;
// }
</style>
