<template>
<div>
  <Clock
    v-bind:secs="time.seconds"
    v-bind:mins="time.minutes"
    v-bind:hrs="time.hours"
   />
  <StartStop
    v-on:start="time.start()"
    v-on:stop="time.pause()"
  />
</div>
</template>

<script>
import Clock from './clock.vue'
import StartStop from './StartStop.vue'

const timeInstance = {
  allSeconds: 0,
  get hours () { return ~~(this.allSeconds / (3600)) },
  get minutes () { return ~~((this.allSeconds % 3600) / 60) },
  get seconds () { return ~~(this.allSeconds % 3600 % 60) },
  interval: false,
  start () {
    this.interval = this.interval || setInterval(() => {
      this.allSeconds++
    }, 1000)
  },
  pause () {
    clearInterval(this.interval)
    this.interval = null
  }
}

export default {
  name: 'MainView',
  data: () => {
    return {
      time: timeInstance
    }
  },
  components: {
    Clock,
    StartStop
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
