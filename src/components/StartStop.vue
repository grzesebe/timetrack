<template>
  <div>
  <button v-on:click="start">Start</button>
  <button v-on:click="stop">Stop</button>
  </div>
</template>

<script>
export default {
  name: 'StartStop',
  data: () => { return { e: 'e' } },
  methods: {
    start: function () {
      this.$emit('start')
    },
    stop: function () {
      this.$emit('stop')
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
